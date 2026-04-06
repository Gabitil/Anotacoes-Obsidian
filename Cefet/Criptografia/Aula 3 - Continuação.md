
A relação $a \equiv b \pmod m$ tem as seguintes propriedades:

1) (Reflexiva) $a \equiv a \pmod m$
2) (Simétrica) Se $a \equiv b \pmod m$, então $b \equiv a \pmod m$
3) (Transitiva) Se $a \equiv b \pmod m$ e $b \equiv c \pmod m$, então $a \equiv c \pmod m$

Uma relação com estas 3 propriedades é uma **relação de equivalência**

Dado $n$, vamos denotar por $\mathbb{Z}_{n}$ o conjunto das classes de equivalência modulo $n$.

$$
\mathbb{Z}_{n}=\{\bar{0},\bar{1},\dots,\overline{n-1} \}
$$
onde $\bar{a}=\{a+k_{n}| k \in \mathbb{Z}\}$

$$
\bar{7} = \{\dots,-8,7,22,37,52,\dots\}=\bar{22}=-\bar{8}
$$

uma forma intuitiva de pensar em $\mathbb{Z}_{n}$ é que colocamos os números em um círculo ao invés de uma reta.

![[Crpt - Ex 3]]

Geralmente representamos $\bar{a}$ usando o menor $a$ natural possível, isto não é necessário.

em $\mathbb{Z}_{15}$

$$
\bar{2}=\bar{47}
$$
$$
\bar{2} . \bar{7}=\bar{14}
$$
$$
\overline{47} . \overline{112}
$$


Exemplo: Calcule o resto na divisão por $7$ de $10^{135}$
$$
\bar{10}=\bar{3}
$$
$$
\overline{10²}= \overline{10} . \overline{10} = \overline{3}. \overline{3} = \overline{2}
$$
$$
\overline{10³}=\overline{10²}.\overline{10}=\overline{2}.\overline{3}=\overline{6}
$$
$$
\overline{10⁴}=\overline{6}.\overline{3}=\overline{4}
$$
$$
\overline{10⁵}=\overline{4}.\overline{3}=\overline{5}
$$
$$
\overline{10⁶}=\overline{5}.\overline{3}=\overline{1}
$$

como $\overline{10⁶}=\bar{1}$, e $135=22.6+3$

então $10^{135}=(10⁶)^{22}.10³ \equiv 1^{22}.10³ \pmod 7$

$$
\overline{1^{22}.10^3}=\overline{10^3}=\overline{6}
$$
$$
10^{135} \equiv 6 \pmod 7
$$

logo o resto é 6.

Exemplo: Encontre o resto na divisão de $3^{64}$ na divisão por 31

$$
3^2 \equiv 9 \pmod{31}
$$
$$
3^3 \equiv 27 \equiv -4 \pmod{31}
$$

como 64=3.21+1

$$
3^{64} \equiv (3^3)^{21}.3 \equiv (-4)^{21}.3 \equiv -(2^{42}).3 \pmod{31}
$$

como $2^5\equiv 32 \equiv 1 \pmod{31}$, então
$$
-(2^{42}).3 \pmod{31} \equiv -(2^{2}).3 \equiv -12 \equiv 19 \pmod{31}
$$

Exemplo:

Calcule o resto de $6^{35}$ na divisão por 16.

$$
6^4=2^4.3^4=16.3^4 \equiv 0 \pmod{16}
$$
$$
6^{35}=6^4.6^31 \equiv 0 \pmod{16}
$$


**Inverso**

Dado $\bar{a} \in \mathbb{Z}_{n}$, dizemos que $\bar{b} \in \mathbb{Z}_{n}$ é um **inverso** de $\bar{a}$ se $\bar{a}.\bar{b}=\bar{1}$

Exemplo: Em $\mathbb{Z}_{7}$

$\bar{1}.\bar{1}=\bar{1}$
$\bar{2}.\bar{4}=\bar{1}$
$\bar{3}.\bar{5}=\bar{1}$
$\bar{6}.\bar{6}=\bar{1}$

### Máximo divisor comum

**lema:** Dados $a$ e $b$ inteiros, então

$mdc(a,b)= mdc(a,b+a)$

Exemplo:

$$
mdc(30-24,24)=mdc(6,24)=mdc(6,18)=mdc(6,12)
$$
$$
=mdc(6,6)=6
$$
### Algoritmo de Euclides

Dados $a$ e $b \in \mathbb{Z}$, para encontrar $mdc(ab)$, basta fazer


$$
a=q_{1}b+r_{1}
$$
$$
b=q_{2}.r_{1}+r_{2}
$$
$$
r_{n-2}=q_{n}.r_{n-1}+r_{n}
$$

$$
mdc(a,b)=mdc(a-q_{1}b,b)=mdc(r_{1},b)=mdc(b,r_{1})
$$
então

$mdc(a,b)=mdc(r_{n-1},0)=r_{n-1}$

Exemplo:

$$
mdc(154,30)=mdc(30,4)=mdc(4,2)
$$

onde o mdc é 2

**Exemplo:**

Vamos calcular o mdc de 10 e 25 usando o algoritmo de euclides

$25/10 (r5,d2)$
$mdc(25,10)=mdc(10,5)$
$10/5=r0,d2$
$mdc(10,5)=mdc(5,0)=5$

$10=5.2+0$
$25=2.10+5$
$5=1.25-2.10$


**Teorema:** $mdc(a,b)$ é o menor número natural que pode ser escrito na forma $k_{1}.a+k_{2}.b$, $k_{1},k_{2} \in \mathbb{Z}$.

dois números $a$ e $b$ são ditos *primos entre si*, ou *coprimos* se $mdc(a,b)=1$.


pelo teorema anterior, $a$ e $b$ são primos entre si se, e somente se, existem $k_{1}$ e $k_{2} \in \mathbb{Z}$ tais que $k_{1}.a+k_{2}.b=1$

 