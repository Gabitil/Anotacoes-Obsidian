
### Exemplo 

a sequência definida por 

$a_{1}=2$ $a_{n+1}=\frac{1}{2}(a_{n}+6)$

$a_{2}=\frac{1}{2}(2+6)=4$ 
$a_{3}=5, a_{4}=\frac{11}{2}$

logo $a_{n+1}>a_{n}$ para todo $n$, portanto é a sequencia decrescente e monótona.

se $a_{n}\leq 6$

$a_{n+1}=\frac{1}{2}(a_{n}+6)\leq \frac{1}{2}(6+6)=6$

logo $a_{n}\leq_{6}$ para todo $n$

pelo teorema da sequência monótona, a sequência é convergente.

seja

$$
L=\lim_{ n \to \infty } a_{n}
$$
$$
= \lim_{ n \to \infty } a_{n+1}= \lim_{ n \to \infty } \frac{1}{2}(a_{n}+6)=\frac{1}{2}\lim_{ n \to \infty } (a_{n})+3= \frac{L}{2}+3
$$
$$
L=\frac{L}{2}+3
$$
$$
L-\frac{L}{2}=3 
$$
$$
\frac{L}{2}=3
$$
$$
L=6
$$

# Séries

Dada uma sequência $a_{n}$, chamamos de série a soma $a_{1},a_{2},\dots,a_{n}+\dots$ e a denotamos por
$$
\sum_{n=1}^{\infty} a_{n}
$$

### Exemplo:

$$
\sum_{n=1}^{\infty} \frac{3}{10^n} =\frac{1}{3}
$$

nem toda série converge

### Exemplo:

$$
\sum_{n=1}^{\infty}n=1+2+3+\dots
$$
diverge

### Exemplo:

$$
\sum_{n=1}^{\infty} (-1)^n 
$$
diverge


Dada a série $\sum_{n=1}^{\infty} a_{n}$, chamamos $s_{n}= a_{1},a_{2},\dots,a_{n}$ de n-ésima soma parcial.
Se a sequência $\{s_{n}\}$  for convergente, dizemos que a série é convergente, e sua soma é $s=\lim_{ n \to \infty }s_{n}$ , ou $\sum_{n=1}^{\infty} a_{n}=s$
Se a sequência $\{s_{n}\}$ é divergente, dizemos que a série é divergente.

### Exemplo

$\sum_{n=1}^{\infty}(-1)^n$ é tal que

$s_{1}=-1$
$s_{2}=0$
$s_{3}=-1$
$s_{4}=0$ 

logo, como a sequência $\{s_{n}\}$ diverge, a série diverge.

### Exemplo

$$
\sum_{n=1}^{\infty} \frac{1}{2^n} =1
$$

$s_{1}=\frac{1}{2}$
$s_{2}=\frac{1}{2}+\frac{1}{4}=\frac{3}{4}$
$s_{3}=\frac{1}{2}+\frac{1}{4}+\frac{1}{8}=\frac{7}{8}$
$\dots$

$\lim_{ n \to \infty } s_{n}=1$

### Exemplo:

$$
\sum_{n=1}^{\infty} ar^{n-1}=
$$
$$
=a+ar+ar^2+\dots+ar^{n-1}+\dots
$$
com $a \ne 0$ 

se $r=\pm 1$, a séria diverge. se $r \ne \pm 1$ 

$s_{n}=a+ar+ar^2+\dots+ar^{n-1}$
$rs_{n}=ar+ar^2+\dots+ar^{n-1}+ar^n$
$s_{n}-rs_{n}=a-ar^n$
$s_{n}(1-r)=a(1-r^n)$
$$
s_{n}=a \cdot \frac{1-r^n}{1-r}
$$
$\lim_{ n \to \infty }s_{n}$ diverge se $r $
