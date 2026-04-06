


Seja uma função contínua, positiva e decrescente em $[k,\infty)$ e seja $a_{n}=f(n)$. Então a série $\sum_{n=1}^\infty a_{n}$ converge se, e somente se, a integral imprópria $\int_{k}^\infty f(x)dx$ converge

### Exemplo:

A série $\sum_{n=1}^{\infty} \frac{1}{n^2}$ é convergente?

$a_{n}=\frac{1}{n^2}$

$f(x)=\frac{1}{x^2}$ é tal que $f(n)=a_{n}$, $f$ é contínua, positiva e decrescente em $[1,\infty)$. Logo, pelo teste da integral $$\sum_{n=1}^{\infty} \frac{1}{n^2}$$ é convergente se, e somente se, $$\int_{1}^\infty \frac{1}{x^2}dx$$ é convergente.

$$
\lim_{ t \to \infty } \int_{1}^t \frac{1}{x^2}dx= \lim_{ t \to \infty } \left[ -\frac{1}{x} \right]_{1}^t= \lim_{ t \to \infty } -\frac{1}{t}+1=1
$$
é convergente. Logo $\sum_{n=1}^{\infty} \frac{1}{n^2}$ converge.

### Exemplo:

Determine se $$
\sum_{n=1}^{\infty} \frac{1}{n^2+1}
$$
é convergente ou divergente.

$$
a_{n} = \frac{1}{n^2+1}
$$
$$
f(x)=\frac{1}{x^2+1}
$$

$f$ é contínua, positiva e decrescente em $[1,\infty)$

$$
\int_{1}^\infty \frac{1}{x^2+1}dx = \lim_{ t \to \infty } [\arctan x]_{1}^t = \lim_{ t \to \infty } \arctan (t)-\arctan(1)= \frac{\pi}{4}
$$