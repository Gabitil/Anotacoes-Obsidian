
$$\int_{-1}^3 [^1]\frac{1}{x} dx = \ln|x|]_{-1}^3 =\ln_{3}-\ln_{1}=\ln_{3}$$

[^1]: Teorema Fundamental do Calculo

Essa integral está errada, pois foi usado o teorema fundamental do calculo.

para usar o teorema fundamental do calculo, a função tem que ser continua e a função $$f(x)=\frac{1}{x}$$
não é continua em $[-1,3]$ , e $f$ não está definido em $f$

portanto pensamos o seguinte:

$$\int_{-1}^0 \frac{1}{x} dx=\lim_{ t \to o^- } \int_{-1}^t\frac{1}{x} dx$$
$$\int_{0}^3 \frac{1}{x}dx= \lim_{ t \to 0^+ } \int_{t}^3 \frac{1}{x}dx $$

$$\int_{-1}^3 \frac{1}{x}dx:= \int_{-1}^0 \frac{1}{x}dx + \int_{0}^3 \frac{1}{x}dx$$

f é continua em $[-1,3]$ exceto em 0.


**Definições:**

Seja, $y=f(x)$ uma função tal que:

$i)$ $f$ é continua em $[a,b)$. Então:

$$\int_{a}^b f(x)dx = \lim_{ t \to b^- } \int_{a}^t f(x)dx $$
$ii)$ $f$ é continua em $(a,b]$. Então:
$$\int_{a}^b f(x)dx = \lim_{ t \to a^+ } \int_{t}^b f(x)dx $$

$iii)$ $f$ é continua em $[a,b]$, exceto em $c \in [a,b]$ Então:
$$\int_{a}^b f(x)dx = \int_{a}^c f(x)dx + \int_{c}^b f(x)dx $$

$iv)$ $f$ é continua e, $[a,\infty)$. Então:

$$\int_{a}^\infty f(x)dx=\lim_{ t \to \infty } \int_{a}^t f(x)dx$$

$v)$ $f$ é continua em $(-\infty,b]$. Então:
$$\int_{-\infty}^b f(x)dx=\lim_{ t \to \infty } \int_{t}^b f(x)dx$$

$vi)$ $f$ é contínua em $(-\infty,\infty)$. Então

$$\int_{-\infty}^\infty f(x)dx = \int_{a}^\infty f(x)dx + \int_{-\infty}^b f(x)dx, a \in \mathbb{R} $$

Essas integrais são ditas integrais impróprias. Caso o limite exista $\mathbb{R}$ dizemos que a integral converge. Caso contrário, dizemos que a integral diverge.


![[Integral de 1 a infinito de 1%x dx]]
![[Integral de menos infinto a 0 de 2x dx]]
