### Seleção de Sensor

- HW611/BMP280
	- Pressão e Temperatura
	- 3.3v
	- Comunicação i2c ou spi - Endereços 0x76 ou 0x77
	- Consumo de corrente (Como não é o ship sozinho e sim um modulo, não confiar nisso): 
		- 36.85 uA no modo High Resolution (não sei se chips paralelos vão até o modo high resolutin, se n tiver é 2.8 uA a 4.16uA)

- GYBMEP/BME280
	- Umidade, pressão e temperatura
	- 3.3v a 5v (tem regulador de tensão imbutido)
	- Comunicação i2c (travado no i2c pq não tem os pinos para ligar o spi, e o endereço ta ou no low padrão (0x76 ) e não tem como mudar)
	- Consumo de corrente (Como não é o chip sozinho e sim um modulo, não confiar nisso): 
		- 1.8 uA @ 1 Hz  medindo só umidade e temperatura
		- 2.8 uA @ 1Hz pressão e temperatura
		- 3.6 uA @ 1Hz umidade, pressão e temperatura
		- 0.1 uA no modo sleep
- GY-273/ QMC5883L
	- Magnetometro
	- 3v ou 5v
	- Comunicação i2c - Endereço 0x0D
	- Consumo de corrente: Max, 2.6 mA (Do chip sozinho, não do modulo, isso tem que verificar)
- GY-521/MPU6050
	- 3.3v ou 5v
	- Acelerometro e giriscopio
	- Comunicação i2C - Endereços 0x68 ou 0x69
	- Consumo de corrente: Max = 3.9 mA (Do chip)
- GY-302
	- Sensor de Luminosidade
	- 3.3v
	- I2C - Endereços 0x23 ou 0x5C
	- Consumo de corrente = 7 mA max (Do ship)
- GY-GPS6MV2 \NEO 6M
	- GPS
	- 3.3v ou 5v
	- UART (TX\RX):
	- obs: Usar alimentação 5v pois o modulo consome muita energia, mas os pinos em si usam 3.3v
	- Consumo de corrente = 45mA (Do modulo finalmente)



o GY-273 vem com uma placa paralela que chama QMC5883L e o endereço é 0x0D

### Pinos do ESP32 utilizados e configuração de endereços:

D22 = SDL;
D21= SDA;
D27= Interruptor do mpu6050
RX2= TX do gps
TX2 = RX do gps

BME - Está conectado no GND por padrão, então o endereço usado é 0x76;

BMB - O SDo foi conectado no 3.3v, fazendo o endereço ser 0x77

GY-273 - Chip paralelo de magnetômetro com a porta sendo 0x0D

GY-521 - O pino AD0 foi conectado no GND, fazendo com que o endereço seja 0x68

GY-302 - O ADDR foi conectado no GND fazendo com que o endereço seja 0x23

### Foto da montagem física
![[WhatsApp Image 2026-04-23 at 16.20.13(1).jpeg]]
![[WhatsApp Image 2026-04-23 at 16.20.13.jpeg]]


### Código utilizado

```cpp
#include <Wire.h>
#include <BMx280I2C.h>
#include <DFRobot_QMC5883.h>
#include "I2Cdev.h"
#include "MPU6050_6Axis_MotionApps20.h"
#include <BH1750_WE.h>
#include <HardwareSerial.h>
#include <TinyGPSPlus.h>

#define BH1750_ADDRESS 0x23
#define BME 0x76
#define BMP 0x77

#define OUTPUT_READABLE_YAWPITCHROLL // MPU6050

static const int RXPin = 16, TXPin = 17;
static const uint32_t GPSBaud = 9600;

//create a BMx280I2C object using the I2C interface with I2C Address 0x76
BMx280I2C bme280(BME);
BMx280I2C bmp280(BMP);
DFRobot_QMC5883 qmc5883(&Wire, 0x0D);
MPU6050 mpu(0X68, &Wire);
BH1750_WE myBH1750 = BH1750_WE(BH1750_ADDRESS); 
TinyGPSPlus gps;

HardwareSerial ss(2); // UART2

int const INTERRUPT_PIN = 27;  // Define the interruption #0 pin
bool blinkState;

/*---MPU6050 Control/Status Variables---*/
bool DMPReady = false;  // Set true if DMP init was successful
uint8_t MPUIntStatus;   // Holds actual interrupt status byte from MPU
uint8_t devStatus;      // Return status after each device operation (0 = success, !0 = error)
uint16_t packetSize;    // Expected DMP packet size (default is 42 bytes)
uint8_t FIFOBuffer[64]; // FIFO storage buffer

/*---Orientation/Motion Variables---*/ 
Quaternion q;           // [w, x, y, z]         Quaternion container
VectorInt16 aa;         // [x, y, z]            Accel sensor measurements
VectorInt16 gy;         // [x, y, z]            Gyro sensor measurements
VectorInt16 aaReal;     // [x, y, z]            Gravity-free accel sensor measurements
VectorInt16 aaWorld;    // [x, y, z]            World-frame accel sensor measurements
VectorFloat gravity;    // [x, y, z]            Gravity vector
float euler[3];         // [psi, theta, phi]    Euler angle container
float ypr[3];           // [yaw, pitch, roll]   Yaw/Pitch/Roll container and gravity vector

/*-Packet structure for InvenSense teapot demo-*/ 
uint8_t teapotPacket[14] = { '$', 0x02, 0, 0, 0, 0, 0, 0, 0, 0, 0x00, 0x00, '\r', '\n' };

/*------Interrupt detection routine------*/
volatile bool MPUInterrupt = false;     // Indicates whether MPU6050 interrupt pin has gone high
void DMPDataReady() {
  MPUInterrupt = true;
}

// This custom version of delay() ensures that the gps object
// is being "fed".
static void smartDelay(unsigned long ms)
{
  unsigned long start = millis();
  do 
  {
    while (ss.available())
      gps.encode(ss.read());
  } while (millis() - start < ms);
}

static void printFloat(float val, bool valid, int len, int prec)
{
  if (!valid)
  {
    while (len-- > 1)
      Serial.print('*');
    Serial.print(' ');
  }
  else
  {
    Serial.print(val, prec);
    int vi = abs((int)val);
    int flen = prec + (val < 0.0 ? 2 : 1); // . and -
    flen += vi >= 1000 ? 4 : vi >= 100 ? 3 : vi >= 10 ? 2 : 1;
    for (int i=flen; i<len; ++i)
      Serial.print(' ');
  }
  smartDelay(0);
}

static void printInt(unsigned long val, bool valid, int len)
{
  char sz[32] = "*****************";
  if (valid)
    sprintf(sz, "%ld", val);
  sz[len] = 0;
  for (int i=strlen(sz); i<len; ++i)
    sz[i] = ' ';
  if (len > 0) 
    sz[len-1] = ' ';
  Serial.print(sz);
  smartDelay(0);
}

static void printDateTime(TinyGPSDate &d, TinyGPSTime &t)
{
  if (!d.isValid())
  {
    Serial.print(F("********** "));
  }
  else
  {
    char sz[32];
    sprintf(sz, "%02d/%02d/%02d ", d.month(), d.day(), d.year());
    Serial.print(sz);
  }
  
  if (!t.isValid())
  {
    Serial.print(F("******** "));
  }
  else
  {
    char sz[32];
    sprintf(sz, "%02d:%02d:%02d ", t.hour(), t.minute(), t.second());
    Serial.print(sz);
  }

  printInt(d.age(), d.isValid(), 5);
  smartDelay(0);
}

static void printStr(const char *str, int len)
{
  int slen = strlen(str);
  for (int i=0; i<len; ++i)
    Serial.print(i<slen ? str[i] : ' ');
  smartDelay(0);
}


void setup() {

    Wire.begin(21,22);

  // put your setup code here, to run once:
	Serial.begin(115200);

	//wait for serial connection to open (only necessary on some boards)
	while (!Serial);


	//begin() checks the Interface, reads the sensor ID (to differentiate between BMP280 and BME280)
	//and reads compensation parameters.
	if (!bme280.begin())
	{
		Serial.println("begin() failed. check your BME280 Interface and I2C Address.");
		while (1);
	}
	
	if (!bmp280.begin())
	{
		Serial.println("begin() failed. check your BMP280 Interface and I2C Address.");
		while (1);
	}

	if (bme280.isBME280())
		Serial.println("sensor is a BME280");
	else
		Serial.println("sensor is a BMP280");

	if (bmp280.isBME280())
		Serial.println("sensor is a BME280");
	else
		Serial.println("sensor is a BMP280");

	//reset sensor to default parameters.
	bme280.resetToDefaults();
	bmp280.resetToDefaults();

	//by default sensing is disabled and must be enabled by setting a non-zero
	//oversampling setting.
	//set an oversampling setting for pressure and temperature measurements. 
	bme280.writeOversamplingPressure(BMx280MI::OSRS_P_x16);
	bme280.writeOversamplingTemperature(BMx280MI::OSRS_T_x16);
	
	bmp280.writeOversamplingPressure(BMx280MI::OSRS_P_x16);
	bmp280.writeOversamplingTemperature(BMx280MI::OSRS_T_x16);

	//if sensor is a BME280, set an oversampling setting for humidity measurements.
	if (bme280.isBME280())
		bme280.writeOversamplingHumidity(BMx280MI::OSRS_H_x16);

	while (!qmc5883.begin())
	{
		Serial.println("Could not find a valid 5883 sensor, check wiring!");
		delay(500);
	}

	if(qmc5883.isQMC())
	{
		Serial.println("Initialize QMC5883");
		// qmc5883.setRange(QMC5883_RANGE_2GA);
		// Serial.print("qmc5883 range is:");
		// Serial.println(qmc5883.getRange());

		// qmc5883.setMeasurementMode(QMC5883_CONTINOUS);
		// Serial.print("qmc5883 measurement mode is:");
		// Serial.println(qmc5883.getMeasurementMode());

		// qmc5883.setDataRate(QMC5883_DATARATE_50HZ);
		// Serial.print("qmc5883 data rate is:");
		// Serial.println(qmc5883.getDataRate());

		// qmc5883.setSamples(QMC5883_SAMPLES_8);
		// Serial.print("qmc5883 samples is:");
		// Serial.println(qmc5883.getSamples());
	}

	/*Initialize device*/
	Serial.println(F("Initializing I2C devices..."));
	mpu.initialize();
	pinMode(INTERRUPT_PIN, INPUT);

	/*Verify connection*/
	Serial.println(F("Testing MPU6050 connection..."));
	if(mpu.testConnection() == false){
		Serial.println("MPU6050 connection failed");
		while(true);
	}
	else {
		Serial.println("MPU6050 connection successful");
	}

	/* Initializate and configure the DMP*/
	Serial.println(F("Initializing DMP..."));
	devStatus = mpu.dmpInitialize();

	/* Supply your gyro offsets here, scaled for min sensitivity */
	mpu.setXGyroOffset(0);
	mpu.setYGyroOffset(0);
	mpu.setZGyroOffset(0);
	mpu.setXAccelOffset(0);
	mpu.setYAccelOffset(0);
	mpu.setZAccelOffset(0);

	/* Making sure it worked (returns 0 if so) */ 
	if (devStatus == 0) {
		mpu.CalibrateAccel(6);  // Calibration Time: generate offsets and calibrate our MPU6050
		mpu.CalibrateGyro(6);
		Serial.println("These are the Active offsets: ");
		mpu.PrintActiveOffsets();
		Serial.println(F("Enabling DMP..."));   //Turning ON DMP
		mpu.setDMPEnabled(true);

		/*Enable Arduino interrupt detection*/
		Serial.print(F("Enabling interrupt detection (Arduino external interrupt "));
		Serial.print(digitalPinToInterrupt(INTERRUPT_PIN));
		Serial.println(F(")..."));
		attachInterrupt(digitalPinToInterrupt(INTERRUPT_PIN), DMPDataReady, RISING);
		MPUIntStatus = mpu.getIntStatus();

		/* Set the DMP Ready flag so the main loop() function knows it is okay to use it */
		Serial.println(F("DMP ready! Waiting for first interrupt..."));
		DMPReady = true;
		packetSize = mpu.dmpGetFIFOPacketSize(); //Get expected DMP packet size for later comparison
	} 
	else {
		Serial.print(F("DMP Initialization failed (code ")); //Print the error code
		Serial.print(devStatus);
		Serial.println(F(")"));
		// 1 = initial memory load failed
		// 2 = DMP configuration updates failed
	}
	pinMode(LED_BUILTIN, OUTPUT);

	if(!myBH1750.init()){ // sets default values: mode = CHM, measuring time factor = 1.0
		Serial.println("Connection to the BH1750 failed");
		Serial.println("Check wiring and I2C address");
		while(1){}
	}
	else{
		Serial.println("BH1750 is connected");
	}

	ss.begin(GPSBaud, SERIAL_8N1, RXPin, TXPin);

	Serial.print(F("Testing TinyGPSPlus library v. ")); Serial.println(TinyGPSPlus::libraryVersion());

}

void loop() {

	static const double LONDON_LAT = 51.508131, LONDON_LON = -0.128002;

	Serial.print(F("******* Valores do GPS******* \n"));
	Serial.print(F("Qnt Sat: "));
	printInt(gps.satellites.value(), gps.satellites.isValid(), 5);
	Serial.println();
	Serial.print(F("HDOP: "));
	printFloat(gps.hdop.hdop(), gps.hdop.isValid(), 6, 1);
	Serial.println();
	Serial.print(F("Latitude: "));
	printFloat(gps.location.lat(), gps.location.isValid(), 11, 6);
	Serial.println();
	Serial.print(F("Longitude: "));
	printFloat(gps.location.lng(), gps.location.isValid(), 12, 6);
	Serial.println();
	Serial.print(F("Age: "));
	printInt(gps.location.age(), gps.location.isValid(), 5);
	Serial.println();
	Serial.print(F("Date/Time: "));
	printDateTime(gps.date, gps.time);
	Serial.println();
	Serial.print(F("Altitude (m): "));
	printFloat(gps.altitude.meters(), gps.altitude.isValid(), 7, 2);
	Serial.println();
	Serial.print(F("Curso (deg): "));
	printFloat(gps.course.deg(), gps.course.isValid(), 7, 2);
	Serial.println();
	Serial.print(F("Velocidade (km/h): "));
	printFloat(gps.speed.kmph(), gps.speed.isValid(), 6, 2);
	Serial.println();
	Serial.print(F("Direção: "));
	printStr(gps.course.isValid() ? TinyGPSPlus::cardinal(gps.course.deg()) : "*** ", 6);
	Serial.println();
	Serial.print(F("Distancia para Londres (km): "));
	unsigned long distanceKmToLondon =
		(unsigned long)TinyGPSPlus::distanceBetween(
		gps.location.lat(),
		gps.location.lng(),
		LONDON_LAT, 
		LONDON_LON) / 1000;
	printInt(distanceKmToLondon, gps.location.isValid(), 9);

	Serial.println();
	Serial.print(F("Curso para Londres (deg): "));

	double courseToLondon =
		TinyGPSPlus::courseTo(
		gps.location.lat(),
		gps.location.lng(),
		LONDON_LAT, 
		LONDON_LON);

	printFloat(courseToLondon, gps.location.isValid(), 7, 2);
	
	const char *cardinalToLondon = TinyGPSPlus::cardinal(courseToLondon);
	Serial.println();
	Serial.print(F("Direção para Londres: "));
	printStr(gps.location.isValid() ? cardinalToLondon : "*** ", 6);
	
	Serial.println();
	Serial.print(F("Qnt de caracteres processados: "));
	printInt(gps.charsProcessed(), true, 6);
	Serial.println();
	Serial.print(F("Qnt de sentenças recebidas: "));
	printInt(gps.sentencesWithFix(), true, 10);
	Serial.println();
	Serial.print(F("Qnt de sentenças com checksum falho: "));
	printInt(gps.failedChecksum(), true, 9);
	Serial.println();
	Serial.println();
	
	smartDelay(1000);

	if (millis() > 5000 && gps.charsProcessed() < 10)
    Serial.println(F("No GPS data received: check wiring"));

	if (!DMPReady) return; // Stop the program if DMP programming fails.
    
	/* Read a packet from FIFO */
	if (mpu.dmpGetCurrentFIFOPacket(FIFOBuffer)) { // Get the Latest packet 
		#ifdef OUTPUT_READABLE_YAWPITCHROLL
		/* Display Euler angles in degrees */
		Serial.println(F("Valores do MPU6050:"));
		mpu.dmpGetQuaternion(&q, FIFOBuffer);
		mpu.dmpGetGravity(&gravity, &q);
		mpu.dmpGetYawPitchRoll(ypr, &q, &gravity);
		Serial.print("ypr\t");
		Serial.print(ypr[0] * 180/M_PI);
		Serial.print("\t");
		Serial.print(ypr[1] * 180/M_PI);
		Serial.print("\t");
		Serial.println(ypr[2] * 180/M_PI);
		Serial.println();
		#endif


	/* Blink LED to indicate activity */
	blinkState = !blinkState;
	digitalWrite(LED_BUILTIN, blinkState);
	}

	delay(1000);

	Serial.println(F("******* Valores do BMx280 *******"));
	//start a measurement
	if (!bme280.measure())
	{
		Serial.println("could not start measurement, is a measurement already running?");
		return;
	}

		if (!bmp280.measure())
	{
		Serial.println("could not start measurement, is a measurement already running?");
		return;
	}

	//wait for the measurement to finish
	do
	{
		delay(100);
	} while (!bme280.hasValue());

		do
	{
		delay(100);
	} while (!bmp280.hasValue());

	Serial.print("BME Pressure: "); Serial.println(bme280.getPressure());
	Serial.print("BME Pressure (64 bit): "); Serial.println(bme280.getPressure64());
	Serial.print("BME Temperature: "); Serial.println(bme280.getTemperature());

	Serial.print("BMP Pressure: "); Serial.println(bmp280.getPressure());
	Serial.print("BMP Pressure (64 bit): "); Serial.println(bmp280.getPressure64());
	Serial.print("BMP Temperature: "); Serial.println(bmp280.getTemperature());

	//important: measurement data is read from the sensor in function hasValue() only. 
	//make sure to call get*() functions only after hasValue() has returned true. 
	if (bme280.isBME280())
	{
		Serial.print("BME Humidity: "); 
		Serial.println(bme280.getHumidity());
	}
	Serial.println();
	// Você pode encontrar a declinação magnética da sua região em: http://magnetic-declination.com/
	//
	// A declinação magnética é o ângulo entre o norte magnético e o norte geográfico real.
	// Esse valor varia dependendo de onde você está no mundo e precisa ser ajustado
	// para que a bússola aponte para o norte geográfico correto.
	//
	// No site, você verá o valor no formato: graus° minutos' (ex: -23° 3' Oeste)
	//   - graus: o número antes do símbolo °  (ex: 23)
	//   - minutos: o número antes do símbolo ' (ex: 3) — é a parte fracionária do grau,
	//              onde 60 minutos = 1 grau (funciona igual a horas e minutos)
	//
	// Se a declinação for WEST (Oeste) → use valor NEGATIVO
	// Se a declinação for EAST (Leste) → use valor POSITIVO
	//
	// Fórmula: (graus + (minutos / 60.0)) / (180.0 / PI)
	// Exemplo para Belo Horizonte (-23° 3' Oeste):
	// float declinationAngle = -(23.0 + (3.0 / 60.0)) / (180.0 / PI);

	float declinationAngle = -(23.0 + (3.0 / 60.0)) / (180.0 / PI);
	qmc5883.setDeclinationAngle(declinationAngle);
	sVector_t mag = qmc5883.readRaw();
	qmc5883.getHeadingDegrees();
	Serial.print("Valores do Magnetometro: \n");
	Serial.print("X:");
	Serial.print(mag.XAxis);
	Serial.print(" Y:");
	Serial.print(mag.YAxis);
	Serial.print(" Z:");
	Serial.println(mag.ZAxis);
	Serial.print("Degress = ");
	Serial.println(mag.HeadingDegress);
	delay(100);

	myBH1750.setMode(OTH); // sets mode and starts measurement
  	/* An OTH and OTH_2 measurement takes ~120 ms. I suggest to wait 
     140 ms to be on the safe side. 
     An OTL measurement takes about 16 ms. I suggest to wait 20 ms
     to be on the safe side. */
	delay(140); // wait for measurement to be completed, change for OTL
	float lightIntensity = myBH1750.getLux();
	Serial.print(F("Valores do Sensor de Luz: \n"));
	Serial.print(F("Light intensity: "));
	Serial.print(lightIntensity);
	Serial.println(F(" Lux"));
}




// //scan de endereços i2c
// #include <Arduino.h>
// #include <Wire.h>

// void setup() {
//   Serial.begin(115200);
//   delay(2000);
//   Wire.begin(21, 22);

//   Serial.println("Scanning I2C...");
//   int found = 0;

//   for (uint8_t addr = 1; addr < 127; addr++) {
//     Wire.beginTransmission(addr);
//     uint8_t error = Wire.endTransmission();

//     if (error == 0) {
//       Serial.print("Dispositivo encontrado: 0x");
//       Serial.println(addr, HEX);
//       found++;
//     }
//   }

//   if (found == 0)
//     Serial.println("Nenhum dispositivo encontrado!");
//   else {
//     Serial.print(found);
//     Serial.println(" dispositivo(s) encontrado(s).");
//   }


// }

// void loop() {}
```

### Resultado:

```
******* Valores do GPS******* 
Qnt Sat: 8    
HDOP: 1.6   
Latitude: -19.939726 
Longitude: -43.998150  
Age: 117  
Date/Time: 04/23/2026 18:31:06 223  
Altitude (m): 904.00 
Curso (deg): 0.00   
Velocidade (km/h): 0.78  
Direção: N     
Distancia para Londres (km): 9019     
Curso para Londres (deg): 25.89  
Direção para Londres: NNE   
Qnt de caracteres processados: 3464  
Qnt de sentenças recebidas: 14        
Qnt de sentenças com checksum falho: 3        

Valores do MPU6050:
ypr     0.10    0.05    -0.11

******* Valores do BMx280 *******
BME Pressure: 91418.00
BME Pressure (64 bit): 91418.50
BME Temperature: 26.25
BMP Pressure: 91423.00
BMP Pressure (64 bit): 91420.81
BMP Temperature: 26.15
BME Humidity: 44.81

Valores do Magnetometro: 
X:628 Y:-736 Z:-62
Degress = 288.18
Valores do Sensor de Luz: 
Light intensity: 525.00 Lux
******* Valores do GPS******* 
Qnt Sat: 8    
HDOP: 1.6   
Latitude: -19.939732 
Longitude: -43.998158  
Age: 3    
Date/Time: 04/23/2026 18:31:10 3    
Altitude (m): 904.20 
Curso (deg): 0.00   
Velocidade (km/h): 1.43  
Direção: N     
Distancia para Londres (km): 9019     
Curso para Londres (deg): 25.89  
Direção para Londres: NNE   
Qnt de caracteres processados: 4473  
Qnt de sentenças recebidas: 19        
Qnt de sentenças com checksum falho: 4        

Valores do MPU6050:
ypr     0.13    0.04    -0.12

******* Valores do BMx280 *******
BME Pressure: 91424.00
BME Pressure (64 bit): 91420.42
BME Temperature: 26.26
BMP Pressure: 91424.00
BMP Pressure (64 bit): 91422.37
BMP Temperature: 26.15
BME Humidity: 44.82

Valores do Magnetometro: 
X:590 Y:-728 Z:-40
Degress = 287.42
Valores do Sensor de Luz: 
Light intensity: 528.33 Lux
******* Valores do GPS******* 
Qnt Sat: 8    
HDOP: 1.6   
Latitude: -19.939734 
Longitude: -43.998158  
Age: 100  
Date/Time: 04/23/2026 18:31:11 1690 
Altitude (m): 904.80 
Curso (deg): 0.00   
Velocidade (km/h): 1.37  
Direção: N     
Distancia para Londres (km): 9019     
Curso para Londres (deg): 25.89  
Direção para Londres: NNE   
Qnt de caracteres processados: 5363  
Qnt de sentenças recebidas: 22        
Qnt de sentenças com checksum falho: 5        

Valores do MPU6050:
ypr     0.16    0.07    -0.06

******* Valores do BMx280 *******
BME Pressure: 91420.00
BME Pressure (64 bit): 91419.65
BME Temperature: 26.25
BMP Pressure: 91421.00
BMP Pressure (64 bit): 91418.91
BMP Temperature: 26.15
BME Humidity: 44.79

Valores do Magnetometro: 
X:597 Y:-711 Z:-45
Degress = 285.97
Valores do Sensor de Luz: 
Light intensity: 529.17 Lux
******* Valores do GPS******* 
Qnt Sat: 8    
HDOP: 1.6   
Latitude: -19.939737 
Longitude: -43.998165  
Age: 3    
Date/Time: 04/23/2026 18:31:14 6    
Altitude (m): 904.50 
Curso (deg): 0.00   
Velocidade (km/h): 1.70  
Direção: N     
Distancia para Londres (km): 9019     
Curso para Londres (deg): 25.89  
Direção para Londres: NNE   
Qnt de caracteres processados: 6179  
Qnt de sentenças recebidas: 26        
Qnt de sentenças com checksum falho: 5        

Valores do MPU6050:
ypr     0.21    0.07    -0.03
```
