
## Tipo 1: intervalos infinitos

Considere a curva $y=\frac{1}{x^2}$. Para qualquer número real $t>1$ , podemos calcular a área entre a curva e o eixo x entre $x=1$ e $x=t$ por

$$
\int_{1}^t \frac{1}{x²}dx = \left[ -\frac{1}{x} \right]_{1}^t = -\frac{1}{t}+1= 1-\frac{1}{t}
$$
Note que a área cresce á medida que t cresce e que 

$$
\lim_{ t \to \infty } \int_{1}^t \frac{1}{x^2}dx = \lim_{ t \to \infty } \left( 1-\frac{1}{t} \right)=1
$$
![[Exemplo 1 Aula n+5]]
### Definição:

**a)** se $\int_{a}^t f(x)dx$ existe para todo $t\geq a$, então 

$$
\int_{a}^\infty f(x)dx = \lim_{ t \to \infty } \int_{a}^t f(x)dx
$$
desde que o limite exista

**b)** Se $\int_{t}^b f(x)dx$ existe para todo $t\leq b$, então

$$
\int_{-\infty}^b f(x)dx = \lim_{ t \to \infty } \int_{t}^b f(x)dx
$$
desde que o limite exista.

> [!NOTE]
> Se os limites correspondentes existem, as integrais 
> 
> $$
> \int_{a}^\infty f(x)dx \text{   e   } \int_{-\infty}^b f(x)dx
> $$
> são ditas **convergentes**. Caso contrário elas são ditas **divergentes.**

**c)** Se ambas $\int_{a}^\infty f(x)dx \text{  e} \int_{-\infty}^{a} f(x)dx$ são convergentes, então definimos 

$$
\int_{-\infty}^{\infty}f(x)dx = \int_{-\infty}^{a} f(x)dx + \int_{a}^\infty f(x)dx 
$$

### Exemplo:

$$
\int_{1}^\infty \frac{1}{x²}dx = \lim_{ t \to \infty } \int_{1}^t \frac{1}{x^2}dx=
$$
$$
\lim_{ t \to \infty } \left( 1-\frac{1}{t} \right)=1
$$

A integral é convergente.