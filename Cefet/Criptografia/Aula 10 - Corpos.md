
Um corpo é um anel comutativo com unidade tal que todo elemento tem inverso multiplicativo

uma outra forma de definir é :

$(\mathbb{K},+,*)$ é um corpo se
$(\mathbb{K},+)$ é um grupo comutativo
$(\mathbb{K}/\{0\},\cdot)$ é um grupo comutativo
$\mathbb{K}$ tem distributividade

Exemplos:

$\mathbb{Z}$ não é um corpo
$\mathbb{Q}$ é um corpo
$\mathbb{R}$ é um corpo
$\mathbb{C}$ é um corpo


$\mathbb{Z}_{p}$ é um corpo com $p$ elementos.

Observação: em um anel, um elemento não pode ser um divisor de 0 e ser invertível

$a\cdot b=0$
$b \ne0$

De fato, se $a$ é divisor de $0$, exite $b$ tal que

$0=a*b$
se $a$ fosse invertível,
$0=a^{-1}\cdot_{0}=a^{-1}\cdot(a\cdot b)$
$=(a^{-1}\cdot a)\cdot b=b$.

Seja $A$ um anel com 1 (ou um corpo). Se existe um $k \in \mathbb{N}$ tal que

$[^1]1+1+\dots+1 =0$

[^1]: $k$ vezes
e este é o menor $k$ tal que isto ocorre, dizemos que $A$ tem característica $k$.
	Se não existe tal $k$, dizemos que $A$ tem característica $0$.

Exemplo:

$\mathbb{R}$ tem característica $0$.

$\mathbb{Z}_{5}$ tem caracteristica $5$.

Se $A$ tem característica $k$ e $a \in A$,

[^2]$a+a+\dots+a$ [^3]$=(1+1+\dots+1)\cdot a=0$

[^2]: $k$

[^3]: $=0$

um corpo finito não pode ter característica $0$

Se um corpo tem característica $k$, então $k$ é um número primo.

De fato, se $k=a\cdot b$, com $a,b\in \mathbb{N}$,

$0=(1+1+\dots+1)=(1+1+\dots+1)(1+1+\dots+1)$
        $k$ vezes      $a$ vezes   $b$ vezes
e neste caso, como $a,b\leq k$, a única possibilidade é $a=k$ e $b=1$ ou $a=1$ e $b=k$

$Z_{n}$ é um corpo se, e somente se, $n$ é primo.

Existem outros corpos finitos?

Sim!

Seja $n$ um número natural.

Existe um corpo com $n$ elementos se, e somente se, $n=p^k$ com $k$ primo.

Dois corpos finitos com o mesmo número de elementos são isomorfos.
O corpo com $q$ elementos é denotado por $\mathbb{F}_{q}$.

$\mathbb{F}_{p}=\mathbb{Z}_{p}$


**Polinómios:**

Seja $\mathbb{K}$ um corpo. Um polinômio sobre $\mathbb{K}$ é uma expressão

$a_{0}+a_{1}x+a_{2}x^2+\dots+a_{n}x^n$,

onde $a_{i}\in \mathbb{K}$ e $x$ é uma indeterminada

o conjunto dos polinômios sobre $k$ é denotado por $k[x]$ e é um anel com as operações de $\mathbb{K}$

Exemplo: em $\mathbb{Z}_{5}[x]$
$(\bar{2}+\bar{4}x+\bar{3}x^2)+(\bar{4}+\bar{3}x+\bar{2}x^2)=$
$\bar{3}+\bar{1}x+\bar{4}x^2+\bar{1}x+\bar{2}x^2+\bar{3}x^3+\bar{2}x^2+\bar{4}x^3+\bar{1}x^4$

Definimos o grau do polinômio como usual.

Se $p(x),q(x)\in \mathbb{F}[x],$ e $gr(p(x))=a$ e $gr(q(x))=b$, então

$gr(p(x)\cdot q(x))=a+b$.