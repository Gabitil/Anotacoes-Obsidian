## Sequências

Um sequência é uma lista ordenada de números .
Trataremos exclusivamente de sequências infinitas $a_{1},a_{2},b_{3},\dots$
A sequência $\{a_{1},b_{2},c_{3},\dots\}$ é  também escrito como $\{a_{n}\}$ ou $\{a_{n}\}_{n=1}^\infty$ 

### Exemplo:

São formas de representar a mesma sequência

$\{\frac{1}{2}, \frac{2}{3}, \frac{3}{4}, \frac{4}{5}, \dots, \frac{n}{n+1},\dots\}$ .  ou
$\{\frac{n}{n+1}\}_{n=1}^\infty$
ou
$a_{n}=\frac{n}{n+1}$
### Exemplo:

Representar a mesma sequência

$$
\left\{ \cos \frac{n\pi}{6} \right\}_{n=0}^\infty
$$
$$
a_{n}=\cos \frac{n\pi}{6}, n\geq_{0}
$$

## Definição

uma sequência $\{a_{n}\}$ tem limite $L$ e escrevemos

$$
\lim_{ n \to \infty } a_{n} = L
$$

ou

$a_{n} \to L$ quando $n \to \infty$ 

se podermos tornar $a_{n}$ tão próximo quanto quisermos de $L$, bastando para isso tornar $n$ suficientemente grande.


> [!NOTE] Definição precisa
> $\lim_{ n \to \infty } a_{n} = L$ se para todo $\varepsilon$, existe $n_{0}$ tal que se $n\geq n_{0}$, então $a_{n} \in (L-\varepsilon,L+\varepsilon)$.

Se $\lim_{ n \to \infty } a_{n}$ existe, dizemos que $a_{n}$ converge. Caso contrário, dizemos que $a_{n}$ diverge.

### Exemplo

$$
\lim_{ n \to \infty } \frac{n}{n+1}=1
$$

## Teorema

Se $\lim_{ x \to \infty } f(x) = L$ e $f(n)=a_{n}$ quando $n$ é um inteiro positivo, então $\lim_{ n \to \infty } a_{n}=L$ 

### Exemplo:

$$
a_{n}=\frac{n}{n+1}
$$
$$
f(x) = \frac{x}{x+1}
$$
é tal que $f(n)=a_{n}$

$$
\lim_{ x \to \infty } \frac{x}{x+1}= \lim_{ x \to \infty } \frac{x}{x} \frac{1}{1+\frac{1}{x}} = 1
$$
### Exemplo:

$a_{n}= \frac{n}{e^n}$ converge ou diverge?

$$
f(x)=\frac{x}{e^x}
$$
$$
\lim_{ x \to \infty } \frac{x}{e^x}= \lim_{ x \to \infty } \frac{1}{e^x} = 0
$$

logo $a_{n}$ converge.

As seguintes propriedades são válidas para o limite de sequências


| $$<br>\lim_{ n \to \infty } (a_{n}+b_{n})=\lim_{ n \to \infty } a_{n} +\lim_{ n \to \infty } b_{n}<br>$$                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| $$<br>\lim_{ n \to \infty } (a_{n}-b_{n})= \lim_{ n \to \infty } a_{n}- \lim_{ n \to \infty } b_{n}<br>$$                                                          |
| $$<br>\lim_{ n \to \infty } C = C<br>$$                                                                                                                            |
| $$<br>\lim_{ n \to \infty } C\cdot a_{n}=C\cdot \lim_{ n \to \infty } a_{n}<br>$$                                                                                  |
| $$<br>\lim_{ n \to \infty } (a_{n}\cdot b_{n}) = \lim_{ n \to \infty } a_{n} \cdot \lim_{ n \to \infty } b_{n}<br>$$                                               |
| se $\lim_{ n \to \infty }b_{n} \ne 0$ então $$<br>\lim_{ n \to \infty } \frac{a_{n}}{b_{n}}= \frac{\lim_{ n \to \infty } a_{n}}{\lim_{ n \to \infty } b_{n}}<br>$$ |
| Se $p>0$ e $a_{n}>0$, então $$<br>\lim_{ n \to \infty } (a_{n}^p)= [\lim_{ n \to \infty } a_{n}]^p<br>$$                                                           |


### Exemplo:

se $a_{n}=\frac{n}{\sqrt{ 10n+1 }}$ , $a_{n}$ converge ou diverge?

$$
\lim_{ n \to \infty } \frac{n}{\sqrt{ 10n+1 }}= \lim_{ n \to \infty } \frac{n}{\sqrt{ n\left( 10+\frac{1}{n} \right) }} = \lim_{ n \to \infty } \frac{\sqrt{ n }\sqrt{ n }}{\sqrt{ n }\sqrt{ 10+\frac{1}{n} }}
$$
$$
= \lim_{ n \to \infty } \frac{\sqrt{ n }}{\sqrt{ 10+\frac{1}{n} }}=\infty
$$
## Teorema do sanduíche (ou do confronto)

se $a_{n}\le b_{n}\leq c_{n}$ para $n\geq n_{0}$ , e se $\lim_{ n \to \infty }a_{n}=\lim_{ n \to \infty } C_{n}=L$, então 
$\lim_{ n \to \infty }b_{n}=L$

### Exemplo:

$$
a_{n}=\frac{(-1)^n}{n}
$$
$$
-\frac{1}{n} \leq a_{n} \leq \frac{1}{n}
$$

$$
\lim_{ n \to \infty } \frac{1}{n}=0
$$
$$
\lim_{ n \to \infty } -\frac{1}{n}= -0
$$

logo, pelo teorema do sanduíche, $\lim_{ n \to \infty } a_{n}=0$

## Teorema

Se $\lim_{ n \to \infty }|a_{n}|=0$, então $\lim_{ n \to \infty }a_{n}=0$

## Demonstração:

$$
-|a_{n}| \leq a_{n} \leq |a_{n}|
$$

Se $\lim_{ n \to \infty } |a_{n}| = 0$, então $\lim_{ n \to \infty } -|a_{n}|=-\lim_{ n \to \infty }|a_{n}|=0$, e pelo teorema do sanduíche, $\lim_{ n \to \infty }a_{n}=0$

### Teorema:

Se $\lim_{ n \to \infty }a_{n}=L$ e se $f$ é uma função contínua em $L$, então $\lim_{ n \to \infty }f(a_{n})=f(L)$.


### Exemplo:

$$
\lim_{ n \to \infty } \sin\left( \frac{\pi}{n} \right)=\sin\left( \lim_{ n \to \infty } \frac{\pi}{n} \right)=\sin(0)=0
$$
## Definição

Uma sequência $a_{n}$ é **crescente** se $a_{n}< a_{n+1}$ para todo $n$. Uma sequência $a_{n}$ é **decrescente** se $a_{n}>a_{n+1}$ para todo $n$. Uma sequência é **monótona**, se for crescente ou decrescente.

## Definição

Uma sequência é **limitada superiormente** se existir um número $M$ tal que $a_{n}\leq M$ para todo $n$.
Uma sequência é **limitada inferiormente** se existir um número $N$ tal que $a_{n}\geq N$ para todo $n$.
Se uma sequencia for limitada inferiormente e superiormente, dizemos que ela é **limitada**.

## Teorema da sequência monótona

Toda sequência monótona e limitada é convergente.
