
#### Exemplo:

Calcule

$$
\int \tan xdx
$$
$$
\int \tan(x)dx = \int \frac{\sin(x)}{\cos(x)}dx=
$$
$$
u=\cos(x)
$$
$$
du=-\sin(x)dx
$$
$$
=-\int \frac{-\sin(x)}{\cos(x)}dx= -\int \frac{1}{u}du
$$
$$
=-\ln|u|+C=\boxed{-\ln|\cos(x)|+C}
$$
$$
=\ln |\frac{1}{\cos(x)}+C= \boxed{\ln|\sec(x)|+C}
$$
#### Exemplo:

Calcule $\int_{0}^4 \sqrt{ 2x+1 }dx$ 

$$
u=2x+1
$$
$$
du=2dx
$$
$$
\int \sqrt{ 2x+1}dx= \frac{1}{2}\int 2\sqrt{ 2x+1 }dx=\frac{1}{2} \int \sqrt{ u }du=
$$
$$
\frac{1}{2} \frac{2}{3} u^{3/2} +C= \frac{1}{3} u^{3/2}+C
$$
$$
\frac{1}{3}(2x+1)^{3/2}+C
$$

$$
\left[ \frac{1}{3} (2x+1)^{3/2}\right]_{0}^4 = \frac{27}{3}-\frac{1}{3}=\boxed{\frac{26}{3}}
$$
*Solução alternativa:*

$$\int_{0}^4 \sqrt{ 2x+1 }dx$$
$$
u=2x+1
$$
$$
x=0 \implies u=1
$$
$$
x=4 \implies u=9
$$
$$
du=2dx
$$
$$
\frac{1}{2} \int_{0}^4 2\sqrt{ 2x+1 }dx= \frac{1}{2} \int_{1}^9\sqrt{ u } du = \frac{1}{2}\left[ \frac{2}{3} u^{3/2} \right]_{1}^9
$$
$$
=\left[ \frac{1}{3} u^{3/2}\right]_{1}^9= \frac{27}{3}-\frac{1}{3}=\boxed{\frac{26}{3}}
$$
#### Exemplo:

$$
\int_{1}^2 \frac{dx}{(3-5x)^2}
$$
$$
u=3-5x
$$
$$
du=-5dx
$$
$$
\frac{1}{-5} \int_{1}^2 -\frac{5dx}{(3-5x)^2}= - \frac{1}{5} \int_{-2}^{-7} \frac{1}{u^2}du= -\frac{1}{5}\left[ -\frac{1}{u} \right]_{-2}^{-7}
$$
$$
=-\frac{1}{5}\left( \frac{1}{7} -\frac{1}{2}\right)=-\frac{1}{5}-\frac{5}{14}=\boxed{\frac{1}{14}}
$$


#### Exemplo:

$$
\int_{1}^e \frac{\ln(x)}{x}dx
$$

$$
u=\ln(x)
$$
$$
du=\frac{1}{x}dx
$$
$$
\int_{u(1)=0}^{u(e)=1} u du=\left[ \frac{u^2}{2} \right]_{0}^1= \frac{1}{2}-0=\frac{1}{2}
$$

### Áreas entre curvas

Para calcular a área entre duas curvas $y=f(x)$ e $y=g(x)$, com $f(x)\geq g(x)$, basta calcular
$$
\int_{a}^b [f(x)-g(x)]dx
$$

![[Exemplo 1 Aula 5|1000]]

$$
\int_{a}^b f(x)dx= A+B-D+E+F
$$
$$
\int_{a}^b g(x)dx=A-C-D+F
$$
$$
\int_{a}^b (f(x)-g(x))dx=B+C+E
$$

#### Exemplo:

Calcule a área da região delimitada acima por $y=e^x$, abaixo por $y=x$, e nos lados por $x=0$ e $x=1$.

$$
\int_{0}^1 (e^x-x)dx= \left[ e^x-\frac{x^2}{2} \right]_{0}^1= \left( e-\frac{1}{2} \right)-(1-0) =\boxed{e-\frac{3}{2}}
$$

#### Exemplo:

Encontre a área da região finita entre as parábolas $y=x^2$ e $y=2x-x^2$

$$
x^2=2x-x^2
$$
$$
2x^2-2x=0 \implies x=0 \text{ ou } x=1
$$
$$
\int_{0}^1[(2x-x²)-(x^2)]dx=
$$
$$
\int_{0}^1 (2x-2x^2)dx=
$$
$$
=\left[ x^2-\frac{2x^3}{3} \right]_{0}^1=\left( 1-\frac{2}{3} \right)-0=\boxed{\frac{1}{3}}
$$
#### Exemplo:

Encontre a área da região delimitada por $y=\sin(x)$, $y=\cos(x), x=0$ e $x=\frac{\pi}{2}$

![[Exemplo 2 Aula 5|1000]]

$$
\int_{0}^{\pi/4} [\cos(x)-\sin(x)]dx+\int_{\pi/4}^{\pi/2} [\sin(x)-\cos(x)]dx
$$
$$
=[\sin(x)+\cos(x)]_{0}^{\pi/4} + [-\cos(x)-\sin(x)]_{\pi/4}^{\pi/2} 
$$
#### Exemplo:

Encontre a área da região entre $y=-x^2-1$ e $y=x-7$
