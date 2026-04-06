

**Técnica 5 - Frações Parciais**



Funciona em um modelo especifico de função:

$$
\int \frac{p(x)}{q(x)}dx, p(x) \text{ e } q(x) \text{são polinómios!}
$$

Exemplo:
$$
\int \frac{x⁴-2x²+4x+1}{x³-x²-x+1}
$$


$$
\int \frac{1}{4x+3}dx =\int \frac{1}{u} \frac{1}{4}du=\frac{1}{4} \int \frac{1}{u}du = \frac{1}{4} \ln|u| +C 
$$
$$
\frac{1}{4}\ln|4x+3|+C
$$

$$
u=4x+3
$$
$$
du=4dx
$$
$$
dx=\frac{1}{4}du
$$

---
1)
$$
\int  \frac{A}{Bx+C}dx= A \int \frac{1}{Bx+C}dx = \frac{A}{B} \ln|Bx+C| +C
$$
2)
$$
\int \frac{1}{x²+A}dx = \frac{1}{\sqrt{ A }}\arctan\left( \frac{x}{\sqrt{ A }} \right)+C
$$
3)
$$
\int \frac{1}{Ax²+Bx+C}dx
$$
Onde $Ax²+Bx+C$ **Não** tem raízes reais. Resolve completando quadrados usando 3)



---

Exemplo:

$$
\int \frac{1}{x²+2x+2}dx = \int \frac{1}{(x+2)²+1}dx= \int \frac{1}{u²+1}du= \arctan u+C = \arctan(x+1)+C
$$


$1x²+2x+2=x²+2x+1-1+2$        $u= x+1$
           $=(x+2)²+1$                     $du=dx$
           


![[Aula 16 - Exemplo 1]]

$$
\int \frac{x⁴-2x²+4x+1}{x³-x²-x+1}
$$

![[Aula 16 - Exemplo p2]]

ou seja

$$
\int \frac{x⁴-2x²+4x+1}{x³-x²-x+1}dx= \int {x+1}\text{ }dx+ \int \frac{4x}{x³-x²-x+1}dx
$$

Calculamos:

$$
4 \int \frac{x}{x³ -x²-x+1}dx
$$

*Fatorando:

$x³-x²-x+1=(x-1)(x²-1)$
$q(x)=x³-x²-x+1=(x-1)(x-1)(x+1)$
                   $=(x-1)²(x+1)$



Quebrar em frações Parciais:

$$
\frac{x}{x³-x²-x+1}= \frac{A}{x-1}+\frac{B}{(x-1)²}+\frac{C}{x+1}
$$
$$
=\frac{A(x-1)(x+1)+B(x+1)+C(x-1)²}{(x-1²)(x+1)}
$$
$x=Ax²-A+Bx+B+Cx²-2Cx+C$
$x=(A+C)x²+(B-2C)x+(C+B-A)$

![[Aula 16 - Exemplo p3]]
Integrar:

$$
\int \frac{x}{x³-x²-x+1}dx = \frac{1}{4} \int \frac{1}{x-1}dx+ \frac{1}{2} \int \frac{1}{(x-1)²}dx - \frac{1}{4} \int \frac{1}{x+1} dx
$$

$$
=\frac{1}{4}\ln|x-1| - \frac{1}{2(x-1)}-\frac{1}{4}\ln|x+1|+C
$$
