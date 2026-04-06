### Nome: Gabriel Augusto de Lima Maia


**1a)**
```sml
fun cube n = n * n * n;
```
**b)**
```sml
fun cuber n:real = n*n*n;
```
**c)** 
```sml
fun forth (a::b::c::d::e)=d;
```
**d)**
```sml
fun min3 (x, y, z) =
	if x <= y andalso x <= z then x
	else if y <= x andalso y <= z then y
	else z;
```
**e)**
```sml
 fun rem2 (a,b,c) = (a,c);
```
**f)**
```sml
fun thirds str =
	let
		val chars = explode str
	in
		hd (tl (tl chars))
	end;
```
**g)**
```sml
fun cycle1 (a::b) = b @ [a];
```
**h)**
```sml
fun sort3 (a:real,b,c) =
	let
		fun insert x [] = [x]
		| insert x (y::ys) = if x <= y then x::y::ys else y::insert x ys
		
		fun sort [] = []
		| sort (x::xs) = insert x (sort xs)
	in
		sort [a,b,c]
	end;
```
**i)**
```sml
fun del3 (a::b::c::d)= (a::b::d);
```

**2a)**
```sml
fun pow (x, 0) = 1.0
	| pow (x, n) = x * pow (x, n-1);
```
**b)**
```sml
fun sqsum 0 = 0
	| sqsum n = n * n + sqsum (n - 1);
```
**c)**
```sml

```
**e)**
```sml
- fun member (_, nil) = false 
= | member (e , (x::xs)) = if x = e then true else member (e , xs); 
```
**g)**
```sml
- fun max (x::xs) =
= let
= 	fun maxhelper(m, nil) = m
= 	|   maxhelper(m, (y::ys)) = if m <= y then maxhelper (y, ys) else maxhelper (m, ys);
= 	in 
= 	    maxhelper (x, xs)
= end;

```

