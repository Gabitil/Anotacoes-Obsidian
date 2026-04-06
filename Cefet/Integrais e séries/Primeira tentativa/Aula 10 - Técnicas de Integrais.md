![[Diferencial de uma função f(x)]]


**Técnica 1: Por substituição**

Exemplo:

$\int x^2\sqrt{ x^3+2 }dx$

não da para resolver pois é uma função composta, se não fosse seria assim:

$\int x^2\sqrt{ x } =\int x^2 x^\left( \frac{1}{2} \right)= \int x^\left( \frac{3}{2} \right) = \left( \frac{x^\left( \frac{5}{2} \right)}{\frac{5}{2}} \right)=\frac{\left( 2x^\left( \frac{5}{2} \right) \right)}{5}+C$


Então podemos considerar que $u=g(x)$
$u=x^3+2$
$du=3x^2dx \implies x^2=\frac{1}{3}du$

então vamos multiplicar na equação $\frac{1}{3}.3$ pois $\frac{3}{3}= 1$

$$
\frac{1}{3}\int \sqrt{ x^3+2 } *3x^2 dx
$$
$$
\frac{1}{3}\int \sqrt{ u } du=\frac{1}{3}\left( \frac{u^\left( \frac{3}{2} \right)}{\frac{3}{2}} \right)+C
$$
$$
=\frac{2}{9}u^\left( \frac{3}{2} \right)+C = \frac{2}{9}(x^3+2)^\left( \frac{3}{4} \right)+C
$$
![[Técnica da Substituição de Integral]]

Exemplos:

1- 
$\int tg(x) dx=?$

$$
\int \tan xdx= \int \frac{\sin x}{\cos x} dx = \int\left( \frac{1}{\cos x} \right)\sin xdx=\int\left( \frac{1}{u} \right)(-du)=-\int\left( \frac{1}{u} \right)du= 
$$
$$
=-\ln|u|+C  =-\ln |\cos x|+C
$$
$$
u=\cos x
$$
$$
du=-\sin xdx\implies \sin xdx=-du
$$

2- 
$$
\int \sin (2x+\pi) dx=\int \sin u \frac{1}{3}du = \frac{1}{3} \int \sin u du= \frac{1}{3} (-\cos u)+C = -\cos \frac{3x+\pi}{3} +C
$$
$$
u=3x+\pi
$$
$$
du=3dx\implies dx=\frac{1}{3}du
$$

![[Média de ln x % x em 1 a e]]


![[Integral de menos infinito a infinito de x elv 3 e elv (-x elv 4) dx]]