	
### Gabriel Augusto de Lima Maia

**1a)** 

```sml
fun il2rl x = map real x;
```
**b)** 

```sml
fun ordList x = map ord x;
```
**c)**

```sml
fun squareList x = map (fn x => x * x) x;
```

**d)**

```sml
fun multPairs x = map (fn (a,b)=> a * b)x;
```

**e)** 
```sml
fun incList xs n = map (fn a => a + n) xs;
```
**f)**
```sml
fun sqSum xs = foldr (fn (a,b) => a*a + b) 0 xs;
```
**g)**

```sml
fun bor x = foldr (fn (a,b) => a orelse b) false x;
```
**h)**

```sml
fun dupList x = foldr (fn(a,b) => a::a::b)[] x;
```
**i)**
```sml
fun myLength x = foldr (fn(_,acc) => 1 + acc) 0 x;
```

**j)**
```sml
fun is2absrl x = map (fn a => real (abs a)) x;
```
**k)**
```sml
fun trueCount x = foldr (fn (a,b) => if a then b+1 else b) 0 x;
```
**l)**
```sml
fun maxPairs x = map (fn (a,b) => if a >b then a else b) x;
```
**m)**
```sml
fun lconcat x = foldr (fn (a,b) => a@b) [] x;
```
**n)**
```sml
fun min (x::xs) = foldr (fn (a,b) => if a < b then a else b ) x xs;
```
**o)**
```sml
fun member (x,xs) = foldr (fn (a,b) => (a=x) orelse b) false xs;
```
**p)**
```sml
fun append x y = foldr (op ::) y x;
```
**q)**
```sml
fun less (x, xs) = foldr (fn (a, b) => if a < x then a :: b else b) [] xs;
```
**r)**
```sml
fun evens xs = foldr (fn (a, b) => if a mod 2 = 0 then a :: b else b) [] xs;
```
**s)**
```sml
fun convert xs = foldr (fn ((a,b),(l1,l2)) => (a::l1, b::l2)) ([],[]) xs;
```
**2a)**
```sml
datatype suit = Hearts | Clubs | Diamonds | Spades;

fun suitname Hearts   = "Hearts"
  | suitname Clubs    = "Clubs"
  | suitname Diamonds = "Diamonds"
  | suitname Spades   = "Spades";
```
**b)**
```sml
datatype number = Int of int | Real of real;

fun plus (Int a) (Int b) = Int (a + b)
  | plus (Real a) (Real b) = Real (a + b)
  | plus (Int a) (Real b) = Real (real a + b)
  | plus (Real a) (Int b) = Real (a + real b);

```

**c)**
```sml
datatype intnest = INT of int | LIST of intnest list;

fun addUp (INT n) = n
  | addUp (LIST xs) = foldr (fn (a, b) => addUp a + b) 0 xs;

```