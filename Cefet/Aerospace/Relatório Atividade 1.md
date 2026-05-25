# Sistema de Semáforo de Pedestre com Arduino

**Nome:** Gabriel Augusto de Lima Maia
**Curso:** Engenharia da Computação
**Data:** 20/04/2026

---

## 1. Introdução

O trabalho tem como objetivo testar o conhecimento geral a cerca de eletrônica embarcada com um projeto de semaforo utilizando arduino

A simulação do circuito foi realizada na plataforma TinkerCad.

---

## 2. Descrição do Funcionamento

O sistema possui dois estados principais, **Vermelho (fechado)**, o  estado inicial padrão e **Verde (aberto)**
### Comportamento:

Inicialmente, o LED vermelho Fica aceso continuamente. Ao pressionar o botão, o LED vermelho pisca por aproximadamente 5 segundos, depois, o LED vermelho é desligado e, em seguida, o LED verde é acionado por aproximadamente 15 segundos que, ao terminar,  o sistema retorna ao estado inicial.

---

## 3. Componentes Utilizados

- Arduino Uno
- 2 LEDs (vermelho e verde)
- 1 botão
- 1 transistor NPN
- Resistores:
    - Resistores para LEDs 220Ω
    - Resistor de base do transistor 2.2kΩ
    - Resistor de pull-down do botão 10kΩ

---

## 4. Dimensionamento dos Componentes

### 4.1 Resistor do LED

Para limitar a corrente no LED, utilizou-se a Lei de Ohm:

$R = (Vfonte - VLED) / I$

Considerando:

- $Vfonte = 5V$
- $VLED ≈ 2V$ (LED vermelho)
- $I = 15 mA (0,015 A)$

$R = (5 - 2) / 0,015 ≈ 200 Ω$

Foi utilizado um resistor  de **$220 Ω$**.

---

### 4.2 Resistor da Base do Transistor

O transistor NPN foi utilizado como chave eletrônica.

Considerando:

- $Vbase ≈ 0,7V$
- $VArduino = 5V$

$R = (5 - 0,7) / Ibase$

Assumindo uma corrente de base de aproximadamente $2 mA$:

$R ≈ 4,3 / 0,002 ≈ 2,15 kΩ$

Foi utilizado um resistor de $2.2kΩ$, garantindo saturação do transistor.

---

### 4.3 Resistor do Botão (Pull-down)

Durante a implementação prática, foi necessário adicionar um resistor de **$10kΩ$** ao pino do botão para garantir funcionamento estável.

Isso ocorre porque, sem esse resistor, o pino de entrada do Arduino fica em estado **flutuante**, ou seja, sem uma referência definida de tensão. Nesse caso, o microcontrolador pode interpretar valores aleatórios (HIGH ou LOW), mesmo sem o botão ser pressionado.

O resistor de $10kΩ$ atua como um **pull-down**, conectando o pino ao GND quando o botão não está pressionado.

Assim:

- Botão solto → pino conectado ao GND → leitura LOW
- Botão pressionado → pino conectado ao $5V$ → leitura HIGH

O valor de $10kΩ$ é utilizado por ser um padrão que garante:

- Baixo consumo de corrente
- Boa estabilidade contra ruídos

A corrente no circuito pode ser estimada por:

$I = V / R = 5 / 10000 = 0,5 mA$

Esse valor é suficientemente baixo para não causar desperdício de energia, mas alto o bastante para manter o sinal estável.

---

## 5. Descrição do Circuito

O circuito foi montado de forma que:

- O LED vermelho é acionado diretamente pelo Arduino
- O LED verde é controlado através de um transistor NPN
- O botão é ligado utilizando o modo `INPUT_PULLUP`, conectando o pino ao GND quando pressionado
    
O transistor atua como chave, permitindo a passagem de corrente entre coletor e emissor quando a base é acionada pelo Arduino.

---

## 6. Código Utilizado

Trecho principal do código:

```cpp
void setup()
{
  pinMode(6, INPUT_PULLUP);
  pinMode(4, OUTPUT);
  pinMode(2, OUTPUT);
}

void loop()
{
  
  if(digitalRead(6) == HIGH){
    
    digitalWrite(2, LOW);
    
    for(int i = 0; i<3; i++){
      digitalWrite(2, HIGH);
      delay(500);

      digitalWrite(2, LOW);
      delay(500);
    }
    
    digitalWrite(4,HIGH);
    delay(15000);
    digitalWrite(4,LOW);
  }
  else{
    digitalWrite(2,HIGH);
    digitalWrite(4,LOW);
  }
 }
```

---

## 7. Resultados

A simulação no TinkerCad apresentou funcionamento correto, atendendo aos requisitos propostos:

- Estado inicial com LED vermelho ativo
- Detecção do botão
- Temporização correta dos estados
- Retorno automático ao estado inicial
    

![[Pasted image 20260420213950.png]]

---
![[Pasted image 20260420214015.png]]

## 8. Conclusão

O projeto permitiu compreender o funcionamento de um sistema embarcado simples, incluindo leitura de entradas digitais, controle de saídas, uso de temporização e aplicação de transistores como chave eletrônica.

Além disso, foi possível consolidar conceitos de eletrônica básica, como Lei de Ohm e polarização de componentes.

---

## 9. Anexos

- Circuito Esquematico:

![[Pasted image 20260420214118.png]]

- Circuito em Ambiente de teste: 

![[Pasted image 20260420214231.png]]