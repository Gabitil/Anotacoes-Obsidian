**Definição:** Um anel é um conjunto não vazio com as operações + e $\cdot$ 

$+ : A \times A \to A$
	$(a,b)\mapsto a+b$

$\cdot:A\times A\to A$
	$(a,b)\mapsto a\cdot b$

que satisfazem as seguintes propriedades

1) **Associatividade da soma:**
   $(a+b)+c=a+(b+c)$
2) **Elemento neutro da soma:**
   Existe $0 \in A$ tal que $a+0=0+a=a$ pra todo $a \in A$.
3) **Inverso aditivo:**
   Para todo $a \in A$, existe $-a \in A$ tal que $-a+a=0$
4) **Comutatividade da soma**
   $a+b=b+a$
5) **Associatividade do produto:**
   $(a\cdot b)\cdot c=a\cdot(b\cdot c)$
6) **Distributividade**
   $a\cdot(b+c)=a\cdot b+a\cdot c$
   $(b+c).a=b\cdot a+c\cdot a$
   
   ---
Se ele satisfaz

7) **Elemento neutro do produto:**
   Existe $1\in A$ tal que $a\cdot 1=1\cdot a=a$,
   
   dizemos que é um anel com unidade.

Se ele satisfaz

8) **Comutatividade do produto:**
   
   $a\cdot b=b*a$,
   
   dizemos que é um anel comutativo

**Exemplos:**

$\mathbb{Z},\mathbb{Q},\mathbb{R},\mathbb{C}$ são anéis

O conjunto das matrizes $m\times m$ é um anel

$(Z_{n},+,\cdot)$ é um anel

um **subanel** de um anel $A$ é um subconjunto $B\leq A$ tal que $B$ com as operações de $A$ é um anel

Exemplo:

$2\mathbb{Z}= \{\dots,-2,0,2,4,\dots\}$ é um subanel de $\mathbb{Z}$

Um **Ideal** $I$ de um anel ~~comutativo~~ é um subanel tal que se $i \in I$, e $a\in A$, então $i\cdot a\in I$.

Exemplo: $2\mathbb{Z}$ é um ideal de $\mathbb{Z}$

~~Exemplo: No anel das matrizes $2\times 2$, o conjunto das matrizes com determinante nulo~~

Seja $A$ um anel e $I$ um ideal de $A$. Podemos definir a relação

$x \equiv y mod I$ se e somente se $x-y\in I$

Exemplo:

Se $A=\mathbb{Z}$, e $I=2\mathbb{Z}$

$a \equiv bmod(2\mathbb{Z}) \Leftrightarrow a-b \in I$
            $\Leftrightarrow a-b \text{ é par}$
            $\Leftrightarrow a-b=2k$

$\{\bar{0},\bar{1}\}=\mathbb{Z}_{2}$.

Exemplo: Se $A=\mathbb{Z}$, e $I=n\mathbb{Z}$

A relação de equivalência acima divide $\mathbb{Z}$ nas classes de $\mathbb{Z}_{n}$


De forma geral, dado um anel $A$, o conjunto das classes de equivalência modulo $I$ forma um anel com as operações "Herdadas" de $A$. Este anel é chamado anel quociente $A/I$.

$\mathbb{Z}/(n\mathbb{Z})=\mathbb{Z}_{n}$

Exemplo:

O conjunto dos polinômios com coeficientes em $\mathbb{R}$ é m anel, denotado $\mathbb{R}[x]$.

$$
3+4x-\frac{1}{2}x^2+x^3
$$
$$
a_{0}+a_{1}x+\dots+a_{n}x^n
$$

O conjunto dos mĺtiplos de $x³$ é m ideal $I$ de $\mathbb{R}[x]$.

$a_{3}x^3+a_{4}x^4+\dots+a_{n}x^n$

$x^3(a_{3}+a_{4}x+\dots+a_{n}x^{n-1})$

$\mathbb{R}[x]/I$ é um anel

$1+2x^2+x^3+x^5$
$-$
$1+2x^2-4x^3+x^4$
$--------------$
$5x^3-x^4+x^5\in I$
$1+2x^2+x^3+x^5\equiv1+2x^2-4x^3+x^4$ $mod I$.

Dois polinômios em $\mathbb{R}[x]$ 

$$
a_{0}+a_{1}x+\dots+a_{n}x^n
$$
$$
b_{0}+b_{1}x+\dots+b_{m}x^m
$$

são congruentes módulo $I$ se, e somente se, $a_{0}=b_{0},a_{1}=b_{1}$ e $a_{2}=b_{2}$.

$\mathbb{R}/I=\{a_{0}+a_{1}x+a_{2}x^2|$
        $x\cdot x^2=0$
        $x^2\cdot x^2=0\}$
$(1+x+x^2)\cdot(2x-x^2)=$
$2x+x^2+x^3 -x^4\equiv 2x+x^2$