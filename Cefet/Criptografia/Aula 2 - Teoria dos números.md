

$\mathbb{N} =\{1,2,3,\dots \}$ é um dos conjuntos dos **números naturais**

$\mathbb{Z} =\{\dots,-2,-1,0,1,2,\dots \}$ é o conjunto dos **números inteiros**

Dados $a,b \in \mathbb{Z}$, dizemos que $a$ **divide** $b$, ou que $a$ é um **divisor** de $b$, e denotamos por $a\mid b$ se existir $c \in \mathbb{Z}$ tal que $b=a.c$.

caso contrário, dizemos que $a$ não divide $b$, e denotamos $a\nmid b$.

Exemplo:

$2 \mid 26$, pois $26=2.13$

$5 \nmid 26$

**Definição:** Um número natural $n$ é dito um número **primo** se $n \neq 1$ e os únicos divisores naturais de $n$ são $1$ e $n$.

Exemplo:

$5$ é primo
$12$ não é primo pois $3 \mid 12$.

### Teorema fundamental da aritimética:

Todo número natural maior que 1 ou é primo, ou pode ser escrito de modo único (a menos de ordem, ou seja, a ordem dos números do produto podem ser diferente, mas os números são os mesmos) como um produto de números primos.

### Lema de Euclides
 
Seja $a,b,p \in \mathbb{Z}$ com $p$ primo. Se $p \mid a.b$, então $p\mid a$ ou $p \mid b$.

### Teorema da Euclides

Existem infinitos números primos.

ideia da demonstração: (demostração por absurdo)

por absurdo, se existem apenas os números $p_{1},p_{2},\dots,p_{k}$
Então $(p_{1}.p_{2}. \dots . p_{k})+1$
não é divisível por nenhum primo

### Divisão EUclidiana:

**Teorema:** Sejam a e b dois número inteiros com $b \neq 0$. Então existem dois inteiros q e r tais que 
$a=bq+r$ com $0\leq r\leq|b|$ 

q e r desta forma são únicos.

Exemplo:

![[Crpt - Ex1]]

$28=5.5+3$

q é chamado de **quociente** e r é chamado de **resto** da divisão

Exemplo:

-46 por 7
$-46 = 7.(-7)+3$

dado um número natural n, ao efetuarmos a divisão euclidiana de qualquer inteiro por n, os únicos restos possíveis são $0,1,2,\dots,n-1$

Exemplo: Os únicos restos possíveis na divisão por 4 são $0,1,2$ ou $3$

Todo número inteiro é de uma das seguintes formas

$4k$
$4k+1$
$4k+2$
$4k+3$

Exemplo: todo quadrado é de forma $4k$ ou $4k+1$.

se $a=4k, a²=16k^2=4(4k^2)$
se $a=4k+1,a^2=16k^2+8k+1=4(4k^2+2k)+1$
se $a=4k+2$, $a^2=16k^2+16k+4= 4(4k²+4k+1)$
se $a=4k+3$   $a²=16k^2+24k+9=16k²+24k+8+1=4(4k²+6k+2)+1$

### Aritmética dos restos

Note que ao somar um número da forma $4k+2$ com um número $4q+3$, obtemos $(4k+2)+(4q+3)=4(k+q)+5=4(k+q)+4+1=4(k+q+1)+1 = 4c+1$

da mesma forma, o resto na divisão por 4 de um produto fica determinado pelos restos dos fatores

$$
(4k+2)(4q+3)=16kq+12k+8q+6
$$
$$
4(4kq+3k+2q+1)+2
$$
Seja   um número natural. dizemos que dois números inteiros são congruentes módulo  e escrevemos 

$$
a \equiv b \pmod m
$$

se a e b deixam o mesmo resto na divisão por $m$

Exemplos:

$39 \equiv 10 \pmod {29}$
$29 \equiv 11 \pmod 6$
$8 \not\equiv 15 \pmod 3$

uma forma equivalente de definir é $a \equiv b \pmod m$ se, e somente se, $m \mid(a-b)$

dado $m \in \mathbb{N}$, os números inteiros podem ser separados em classes quanto ao seu resto na divisão $m$. haverão $m$ classes:
$\bar{a}=${números que deixam resto $a$ na divisão por $m$}

$\bar{0},\bar{1},\bar{2},\dots,\overline{m-1}$
$\bar{0}=\{\dots,-m,0,m,2m,\dots\}$
$\bar{1}=\{\dots,-m+1,1,m+1,2m+1,\dots \}$

$\overline{m-1}=\{\dots,-m-1,-1,m-1,2m-1,3m-1,\dots \}$


Dadas as classes modulo, podemos definir uma soma e um produto (que na verdade são as operações herdadas de $\mathbb{Z}$).

Exemplo:

módulo 4, temos as classes $\bar{0},\bar{1},\bar{2},\bar{3}$

![[Crpt - Ex2]]

![[Crpt - Ex3]]

Exercício:

Faça as tabelas de + e . para as classes módulo 6 e módulo 7.