
Se $f$ é contínua em $[a,b]$ e derivável em $(a,b)$,

$$
\int_{a}^b f'(x)dx= f(b)-f(a)
$$
#### Exemplo:

Se $v(t)$ é a velocidade de um carro, como $v$ é a taxa de variação da posição, pelo teorema da variação total

$$
\int_{a}^b v(t)dt = P_{final}-P_{inicial}= \text{Variação da posição}
$$
#### Exemplo:

Se $V(t)$ é o volume de um reservatório de água, então

$$
\int_{a}^b V'(t)dt=V(b)-V(a)= \text{variação do volume}
$$
#### Exemplo:

Se uma partícula se move ao longo de uma reta de forma que sua velocidade no tempo $t$ é $v(t)=t^2- t-6$.

a) Encontre a variação da posição de $t=1$ até $t=4$.

$$
\int_{1}^4 (t²-t-6) dt = \left[ \frac{t^3}{3}-t^2-6t \right]_{1}^4
$$
$$
= \left( \frac{64}{3}-8-24 \right)-(\frac{1}{3}-1-6)=
$$
$$
\frac{128-48-144-2+3+36}{6}= -\frac{27}{6}=\boxed{-\frac{9}{2}}
$$


b) Calcule a distância total percorrida de $t=1$ a $t=4$.
$$
t^2-t-6=0 \implies t=3 \text{, onde tem a interseção da parabola}
$$
$$
\int_{1}^3 (t^2-t-6) dt=  \left[ \frac{t^3}{3}-t^2-6t \right]_{1}^3
$$
$$
=\left( 9-\frac{3}{2}-18 \right)-\left( \frac{1}{3}-\frac{1}{2}-6 \right)= \frac{54-27-108-2+3+36}{6} = -\frac{44}{6}
$$
$$
\int_{3}^4 (t^2-t-6) dt=  \left[ \frac{t^3}{3}-t^2-6t \right]_{3}^4
$$
$$
=\left( \frac{64}{3}-8-24 \right)-\left( 9-\frac{9}{2}-18 \right) =
$$
$$
 \frac{128-48-144-54+27+108}{6}= \frac{17}{6}
$$

$$
\frac{44}{6}+\frac{17}{6} = \boxed{\frac{61}{6}}
$$
## Regra da substituição

Partindo da regra da cadeia, que diz que $f'(g(x))\cdot g'(x)=[f(g(x))]'$, e integrando os dois lados

$$
\int {f'(g(x))\cdot g'(x)dx}=f(g(x))+C
$$
**Regra da substituição:** Se $u=g(x)$ é uma função derivável cuja imagem é um intervalo $I$, e se $f$ é contínua em $I$, então

$$
\int {f(g(x))g'(x)dx}= \int f(u)du
$$

#### Exemplo:

Calcule $\int {x^3 \cos(x^4+2)dx}$
$$
u=x^4+2
$$
$$
du=4x^3dx
$$
$$
\int {x^3 \cos(x^4+2)}dx= \int {\frac{1}{4}\cdot 4x^3\cos(x^4+2)dx}
$$
$$
=\frac{1}{4} \int 4x^3 \cos(x^4+2)dx= \frac{1}{4}\int \cos(u)du
$$
$$
=\frac{1}{4}\sin(u)+C= \boxed{\frac{1}{4}\sin(x^4+2)+C}
$$

#### Exemplo:

Calcule $\int{\sqrt{ 2x+1 }}dx$
$$
u=2x+1
$$
$$
du=2dx
$$
$$
=\frac{1}{2} \int 2 \sqrt{ 2x+1 }dx = \frac{1}{2} \int 2 \sqrt{ u }du
$$
$$
=\frac{1}{2} \frac{u^{3/2}}{\frac{3}{2}}+C= \frac{1}{2}\cdot \frac{2}{3}(2x+1)^{3/2}+C
$$
$$
\boxed{\frac{1}{3}(2x+1)^{2/3}+C}
$$
#### Exemplo:

Calcule $\int e^{5x}dx$

$$
u=5x
$$
$$
du=5dx
$$
$$
= \frac{1}{5} \int 5e^{5x}dx = \frac{1}{5}\int e^u du = \boxed{\frac{1}{5}e^{5x}+C}
$$

#### Exemplo:

Calcule

$$
\int {\sqrt{ 1+x^2 }\cdot x⁵dx}
$$
$$
u=1+x^2 \implies x^2=u-1
$$
$$
du=2xdx
$$

$$
=\frac{1}{2}\int{2x\sqrt{ 1+x^2 }x^4dx}=\frac{1}{2}\int \sqrt{ u }\cdot x^4 du
$$
$$
=\frac{1}{2} \int \sqrt{ u} (u-1)^2du= \frac{1}{2} \int u^{1/2}(u^2-2u+1)du
$$
$$
=\frac{1}{2}\int(u^{5/2}-2u^{3/2}+u^{1/2})= \frac{1}{2}\left[ \frac{u^{7/2}}{\frac{7}{2}}-2 \frac{u^{5/2}}{\frac{5}{2}}+ \frac{u^{3/2}}{\frac{3}{2}} \right]+C
$$
$$
=\frac{1}{2}\cdot \frac{2}{7} u^{7/2} -\frac{1}{2}\cdot 2 \cdot \frac{2}{5} u^{5/2}+\frac{1}{2}\cdot \frac{2}{3}u^{3/2}+C
$$
$$
\frac{u^{7/2}}{7}-\frac{2}{5}u^{5/2}+\frac{1}{3}u^{3/2}+C
$$
$$
\boxed{\frac{(1+x^2)^{7/2}}{7}-\frac{2}{5}(1+x^2)^{5/2}+\frac{1}{3}(1+x^2)^{3/2}+C}
$$



