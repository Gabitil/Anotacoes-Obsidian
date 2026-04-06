
#### Exemplo:

Encontre o volume do sólido obtido ao girar a região limitada entre $y=x^2$ e $y=x$ em torno de $y=2$.
![[Exemplo 1 Aula 6|1000]]
 $$
A(x)= \pi \cdot (2-x^2)^2- \pi(2-x)^2=
$$
$$
\pi(4-4x^2 + x^4)-\pi (4-4x+x^2)=
$$
$$
\pi (x^4-5x^2+4x)
$$
$$
V= \int_{0}^1 A(x)dx= \int_{0}^1 \pi(x^4-5x^2+4x)=
$$
$$
\pi\left[ \frac{x^5}{5}-\frac{5x^3}{3}+\frac{4x^2}{2} \right]_{0}^1
$$
$$
= \pi \left( \frac{1}{5}-\frac{5}{3}+2 \right) = \boxed{\frac{8}{15}\pi}
$$

### Volumes por casacas cilíndricas

Suponha, por exemplo, que queremos calcular o volume do sólido obtido ao girar a região finita entre $y=2x^2-x^3$ e $y=0$ em torno do eixo $y$.

![[Exemplo 2 Aula 6|1000]]

Podemos aproximar o solido por cascas cilíndricas

![[Exemplo 3 Aula 6]]

O volume dessa casca cilíndrica é 

$$
\pi r_{2}^2\cdot h-\pi r_{1}^2h=\pi h(r_{2}^2 -r_{1}^2)=
$$
$$
\pi h (r_{2}+r_{1})(r_{2}-r_{1})=
$$
$$
2\pi h\left( \frac{r_{2}+r_{1}}{2} \right)(r_{2}-r_{1})
$$

$$
r=\left( \frac{r_{2}+r_{1}}{2} \right)
$$
$$
\nabla r = (r_{2}-r_{1})
$$

$$
=2 \pi h r \nabla r
$$

Dividindo o sólido em $m$ cascas de mesma espessura, o volume total é aproximado por

$$
v ≃ \sum_{i=1}^n 2\pi f(x_{i})x_{1}\nabla x 
$$

Tomando o limite quando $n\to \infty$, obtemos

$$
V = \lim_{ n \to \infty } \sum_{i=1}^n 2\pi f(x_{i})x_{1}\nabla x =
$$
$$
\int_{a}^b 2\pi xf(x)dx
$$

Voltando ao exemplo

$$
V = \int_{0}^2 2\pi x(2x^2-x^3)dx= 2\pi \int_{0}^2(2x^3-x^4)dx =
$$
$$
2\pi\left[ \frac{2x^4}{4} - \frac{x^5}{5} \right]_{0}^2= 2\pi\left( \frac{32}{4}-\frac{32}{5} \right)=
$$
$$
2\pi\cdot \frac{32}{20}= \boxed{\frac{16\pi}{5}}
$$

#### Exemplo:

Use cascas cilíndricas para encontrar o volume do sólido obtido pela rotação em torno do eixo $x$ da região entre o eixo $x$ e a curva $y=\sqrt{ x }$ de $x=0$ a $x=1$.

![[Exemplo 4 Aula 6]]

$$
2\pi rh=2\pi\cdot y\cdot (1-y^2)
$$

$$
\int_{0}^1 2\pi y(1-y^2)dy=2\pi = \int_{0}^1 (y-y^3)dy=
$$
$$
= 2\pi\left[ \frac{y^2}{2} - \frac{y^4}{4} \right]_{0}^1= 2\pi \cdot \frac{1}{4} = \boxed{\frac{\pi}{2}}
$$
