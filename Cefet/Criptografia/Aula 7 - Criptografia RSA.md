
### Pré - codificação

A primeira coisa a se fazer é converter a mensagem em números, podemos usar tabelas como no codigo de cesar ou ASCII

O número de algarismos nós simbolos tem que ser constante para evitar ambiguidades

vamos usar dois primos p e q e n=pq.

Suponha que $p=11$, $q=13$ e $n=143$.


Vamos quebrar a mensagem em blocos de tamanhos "arbitrários".

Os blocos não podem começar com 0. Os blocos também devem conter números menores que n.

72/40/30/1/95/113

OS blocos não correspondem a símbolos. Isto impede a análise de frequência.

**Codificação:**

Vamos escolher um número e que seja invertível modulo

$\phi(n)$ (ou seja, $mdc(e,\phi(n))=1$).

$p=11, q=13, n=143.$
$\phi(n)=\phi(p.q)=\phi(p).\phi(q)=(p-1)(q-1)=10.12=120.$

$e=7$  <-- o menor que funciona

$(n,e)$ é a **chave de codificação** do sistema RSA. $(143,7)$

$e=7$ é uma escolha, ele tem que ser um numero que é primo entre si com 120.

Cada bloco é codificado separadamente
Se $b$ é um bloco, denotaremos por $C(b)$ o bloco codificado

$C(b)=$ resto da divisão de $b^e$ por n

pegando o bloco 72


$72²=5184 \equiv 36 mod 143$
$72^4\equiv 36^2 = 1296 \equiv 9mod143$
$72^4.72^2= 9.36 \equiv 38mod143$
$72^7\equiv 38.72 \equiv 19mod143$
então $b=72$ e $C(b)=19$

Para decodificar precisamos de $n$ e do inverso de $e$ em $u(\phi(n))$, vamos chamar este inverso de $d$.

$120=7.17+1\implies 1=120+7(-17)$

$d=103=120-17$

dado um bloco a da mensagem codificada, calculamos $D(a)$ por 

$D(a)$= resto da divisão de $a^d$ por $n$.

Note que $D(C(b))=$ resto da divisão de $(b^e)^d$ por $n$.

$(b^e)^d= b^{ed}=b^{k\phi(n)+1}$

**TEorema de Euler**

Se $b$ é primo com $\phi(n)$

$b^{\phi(n)}\equiv1modn$

