
# Frações Parciais

### Exemplo:

calcule

$$
\int\left( \frac{2}{x-1} - \frac{1}{x+2} \right)dx
$$
$$
= \int \frac{2}{x-1}dx - \int\frac{1}{x+2}
$$
$$
= 2\ln|x-1| - \ln|x+2| + C
$$

### Exemplo:

Calcule

$$
\int \frac{x+5}{x^2+x-2}dx
$$
$$
\frac{2}{x-1} - \frac{1}{x+2} = \frac{2(x+2)-1(x-1)}{(x-1)(x+2)} = \frac{x+5}{x^2+x-2}
$$

logo

$$
\int \frac{x+5}{x^2+x-2}dx = 2\ln|x-1| - \ln|x+2| + C
$$

o método das funções parciais transforma uma função racional $\frac{P(x)}{Q(x)}$ em uma forma mais fácil de ser integrada

**Passo 1:** se $\frac{P(x)}{Q(x)}$ é tal que $gr(P(x))\geq gr(Q(x))$, fazemos uma divisão de polinômios.

### Exemplo:

$$
\int \frac{(x^3+x)}{x-1}dx
$$
$$
(x^3+x) \div (x-1) = x^2+x+2 (\text{resto = 2})
$$
$$
x^3+x=(x-1)(x^2+x+2)+2
$$
$$
\frac{x^3+x}{x-1}=x^2+x+2+\frac{2}{x-1}
$$
integrando obtemos:

$$
\int \left( x^2+x+2+\frac{2}{x-1} \right)dx
$$
$$
=\frac{x^3}{3}+\frac{x^2}{2}+2x+2\ln|x-1| +C
$$
**Passo 2:** Fatorar o denominador $Q(x)$ o máximo possível.

**Passo 3-Caso 1:** Se $\frac{P(x)}{Q(x)}$ é tal que $Q(x)$ é um produto de fatores distintos de grau 1, $ax_{1}+b_{1}$, escrevemos

$$
\frac{P(x)}{Q(x)}=\frac{A_{1}}{ax_{1}+b_{1}}+\frac{A_{2}}{ax_{2}+b_{2}}+\dots+\frac{A_{k}}{ax_{k}+b_{k}}
$$
### Exemplo:

$$
\int \frac{x^2-2x-1}{2x^3-3x^2-2x}dx
$$
$$
2x^3-3x^2-2x = x (2x^2-3x-2)= 2x(x-2)\left( x+\frac{1}{2} \right)
$$
$$
=x(x-2)(2x+1)
$$
$$
\frac{x^2-2x-1}{2x^3-3x^2-2x} = \frac{A}{x}+\frac{B}{x-2}+\frac{C}{2x+1}
$$
$$
=\frac{A(x-2)(2x+1)}{x(x-2)(2x+1)}+\frac{B(x)(2x+1)}{(x-2)(x)(2x+1)}+\frac{C(x)(x-2)}{(2x+1)x(x-2)}
$$
$$
=\frac{A(x-2)(2x+1)+B(x)(2x+1)+C(x)(x-2)}{x(x-2)(2x+1)}
$$
$$
= \frac{x^2 (2A+2B+C)+x(-3A+B-2C)+(-2A)}{2x^3-3x^2-2x}
$$
$$

$$**Passo 3-Caso 2:**  Se há fatores de grau 2 em $Q(x)$, $a_{1}x^2+b_{1}x+c$, então usamos $\frac{A_{i}x+B}{a_{i}x^2+b_{i}x+c}$ no lugar de $\frac{A_{i}}{a_{i}x+b}$

**Passo 3 - Caso 3:** Se $Q(x)$ tem um fator que se repete $r$ vezes, usamos suas potências de 1 a $r$ na decomposição
