
![[Exemplo 1 Aula 3|500]]

$$
\int_{a}^b f(x)dx = \textcolor{blue}{Área} - \textcolor{green}{Área}
$$

$$
\int_{a}^b f(x)dx= F(b)-F(a)= [f(x)]_{a}^b
$$
$$
F'(x)=f(x)
$$

#### Exemplo:

Calcule $\int_{1}^3 e^xdx$

$$
\int_{1}^3 e^xdx = [e^x]_{1}^3=e^3-e^1
$$
#### Exemplo:

Encontre a área sob a curva $y= \cos x$ entre $x=0$ e $x=\frac{\pi}{2}$

$$
\int_{0}^{\pi/2} \cos (x)dx=[\sin(x)]_{0}^{\pi/2}
$$
$$
=\sin\left( \frac{\pi}{2} \right)-\sin(0)=1-0=1
$$
#### Exemplo:

Calcule $\int_{0}^{\pi} \cos (x)dx$

$$
\int_{0}^\pi \cos(x)dx= [\sin(x)]_{0}^\pi 
$$
$$
=\sin \pi-\sin 0=0-0=0
$$
#### Exemplo:

$$
f(x)=
\begin{cases}
x \text{ se } x<1\\
10 \text{ se } x\geq 1
\end{cases}
$$
calcule $\int_{0}^2 f(x)dx$

![[Exemplo 2 Aula 3]]


Não pode ser feito por não entra na definição do teorema fundamental do calculo que diz que a função tem que ser continua para ser integrada.


# Integrais Indefinidas

Vamos escrever a integral definida de f(x)

$$
\int f(x)dx
$$
Para denotar a primitiva mais geral de $f$, isto é, 

$$
\int f(x)dx=F(x)+C \text{, onde } F'(x)=f(x)
$$
#### Exemplo:

$$
\int x^2dx = \frac{x^3}{3}+C
$$

## Tabela de Integrais Indefinidas


| $\int c\cdot f(x)dx$              | $= c\cdot \int f(x)dx$                  |
| --------------------------------- | --------------------------------------- |
| $\int[f(x)+g(x)]dx$               | $= \int f(x)dx + \int g(x)dx$           |
| $\int kdx$                        | $= \int kx+C$, $k$ é constante          |
| $\int x^n dx$                     | $= \frac{x^{n+1}}{n+1} +C$, $n \neq -1$ |
| $\int \frac{1}{x}dx$              | $= \ln \|x\| +C$                        |
| $\int e^x$                        | $= e^x +C$                              |
| $\int a^xdx$                      | $= \frac{a^x}{\ln(a)}+C$                |
| $\int \sin(x)dx$                  | $=-\cos(x)+C$                           |
| $\int \cos(x)dx$                  | $= \sin(x)+C$                           |
| $\int \sec^2(x)dx$                | $=tg(x)+C$                              |
| $\int \csc^2(x)dx$                | $=- \cot(x)+C$                          |
| $\int \sec\cdot \tan(x)$          | $=\sec(x)+C$                            |
| $\int \csc(x)\cdot \cot(x)$       | $=-\csc(x)+C$                           |
| $\int \frac{1}{x^2+1}dx$          | $= \arctan(x)+C$                        |
| $\int \frac{1}{\sqrt{ 1-x^2 }}dx$ | $=\arcsin(x)+C$                         |
| $\int \sinh(x) dx$                | $= \cosh(x)+C$                          |
| $\int \cosh(x)dx$                 | $= \sinh(x)+C$                          |
| $\int \tan (x)dx$                 | $= \ln\|\sec x\|+C$                     |

#### Exemplo:

Calcule $\int [10x^4-2\sec^2(x)]dx$

$$
\int 10x^4dx + \int-2\sec^2(x)dx
$$
$$
= 10 \int x^4 dx - 2 \int \sec^2(x)dx=
$$
$$
=10\left( \frac{x^5}{5} +C_{1} \right) -2 (\tan(x)+C_{2})=
$$
$$
=2x^5-2tg(x)+C
$$

#### Exemplo:

Calcule $\int e^{3x}dx$

$$
e^{3x}= (e^3)^x
$$
$$
\int e^{3x}dx = \frac{e^{3x}}{\ln(e^3)}+C = \frac{e^{3x}}{3}+C
$$

#### Exemplo:

calcule $\int \sin(2x)$

$$
[\cos(2x)]' = -2\sin(2x)
$$
$$
\left[ - \frac{\cos(2x)}{2} \right]'=\sin(2x)
$$
$$
\int \sin(2x)dx = - \frac{\cos(2x)}{2}+C
$$
