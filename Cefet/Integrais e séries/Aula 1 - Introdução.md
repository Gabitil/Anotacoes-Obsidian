

Bibliografia: Calculo- James Stewart.

---
# Integrais

## Áreas

Podemos definir a área de um triângulo e, a partir dela, definir a área de um polígono qualquer.


![[Exemplo 1 Aula 1|3000]]

Dado um círculo, ou qualquer figura, podemos cobri-lo, com sobra, usando quadrados. A área do círculo será menor que a soma das áreas dos quadrados usados. De maneira similar, se um conjunto de quadrados cabe dentro do círculo, sua área será maior que a soma das áreas dos quadrados.

Exemplo: use retângulos para estimar a área entre a parábola $y=x²$ e as retas $y=0$ e $x=1$ .

![[Exemplo 2 Aula 1|500]]

Vamos estimar a área "por cima" e "por baixo"

![[Exemplo 3 Aula 1|500]]


$$Área < \frac{1}{m}\left( \frac{1}{m} \right)^2 +\frac{1}{m}\left( \frac{1}{m} \right)^2 + \dots+\frac{1}{m}\left( \frac{m}{m} \right)^2$$
$$= \frac{1}{m^3}(1^2+2^2+3^2+\dots+m^2)$$
$$\frac{1}{m^3} \frac{m(m+1)(2m+1)}{6}$$
$$
\frac{2m^3+3m^2+m}{6m^3}
$$

Fazendo:

$$
f(x)= \frac{2m^3+3m^2+m}{6m^3}
$$

$$
\lim_{ x \to \infty } \frac{2m^3+3m^2+m}{6m^3} = \frac{2}{6} = \frac{1}{3}
$$

$$
Área \leq \frac{1}{3}
$$
Fazendo o mesmo com a estimativa para baixo, obtemos uma outra função cujo limite quando $x\to \infty$ também é $\frac{1}{3}$, logo $Área \geq \frac{1}{3}$.

Portanto a área da figura é $\frac{1}{3}$.

De forma geral, se queremos calcular a área da região $\int$ sob um gráfico de função 

$y=f(x)$ $(f(x)\geq 0)$, acima do eixo x, e entre $x=a$ e $x = b$

![[Exemplo 4 Aula 1]]

Começamos por dividir $\int$ em m faixas $\int_{1}, \int_{2}, \dots,\int_{m}$ onde a faixa $\int_{i}$ é delimitada por $x_{(i-1)}$ e $x_{i}$, com $x_{0}=a$ e $x_{m}=b$.

![[Exemplo 5 Aula 1|500]]
Vamos fazer isto de forma que as larguras das faixas sejam iguais, ou seja $x_{i+1}-x_{i}=\frac{b-a}{m}$

vamos chamar $\frac{b-a}{m}$ de $\Delta x$

A área de cada faixa é estimada por $f(x_{i})\Delta x$

A área da região $\int$ é definida como

$$
\lim_{ n \to \infty } \sum_{i=1}^n f(x_{i})\Delta x
$$

> [!NOTE] Observação
> Se usarmos no lugar de $f(x_{i})$, $f(x_{i}^*)$, onde $x_{i-1}<x_{i}^*<x_{i}$, o resultado do limite é o mesmo,


# Integral definida

**Definição:** Se $f$ é uma função definida em $a\leq x\leq b$ , dividimos o intervalo $[a,b]$ em $m$ subintervalos de comprimentos iguais $\Delta x=\frac{b-a}{m}$. Sejam $x_{0}=a,x_{1},x_{2},\dots,x_{m}=b$
as extremidades do subintervalos, e sejam $x_{1}^*,x_{2}^*,\dots,x_{m}^*$ tais que $x_{i-1}\leq x_{i}^*\leq x_{i}$. Então a *Integral Definida* de $f$ de $a$ até $b$ é

$$
\int_{a}^b f(x)dx= \lim_{ n \to \infty } \sum_{i=1}^n f(x_{i}^*)\Delta x
$$

==Se o limite existir.==

Caso o limite exista, dizemos que a função é *integrável*.

**Teorema:** Se $f$ é contínua em $[a,b]$, ou se $f$ tem um número finito de descontinuidades, então $f$ é integrável.

**Teorema:** Se $f$ é integrável em $[a,b]$,então:

$$
\int_{a}^b f(x)dx= \lim_{ n \to \infty } \sum_{i=1}^n f(x)\Delta x
$$

