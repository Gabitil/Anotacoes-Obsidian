
Em $\mathbb{Z}_{n}$ nem todo elemento tem inversa multiplicativa, por exemplo, em $\mathbb{Z}_{6}$, $\bar{2}$ não tem inverso.

se $\bar{a}.\bar{b}=1$ em $\mathbb{Z}_{n}$

$(a+k_{n}).(b+q_{n})=1+r_{n}$

o que implica que 

$ab+s_{n}=1+r_{n}$
$ab+t_{n}=1$

e portanto $mdc(a,n)=1$

Se a classe $\bar{a} \in \mathbb{Z}$ não tem inverso, e $0\leq a<n$, e $mdc(a,n)\neq 1$, então $\bar{a}. \overline{\frac{n}{mdc(a,n)}}=\bar{0}$   

Em $\mathbb{Z}_{n}$ não necessariamente vale a lei do cancelamento pois nem toda classe tem inverso.

---
**Exemplo**

em $\mathbb{Z}_{10}$

$\bar{8}.\bar{6}=\bar{8}.\bar{1}=\bar{8}$

mas $\bar{6}\ne \bar{1}$

---
Em $\mathbb{Z}_{p}$, onde $p$ é primo a única classe que não tem inverso é $\bar{0}$

### Pequeno teorema de Fermat

Seja $a$ um inteiro e $p$ um primo.

Então
		$a^p\equiv a\pmod{p}$.

Antes de demonstrá-lo, vamos precisar do seguinte lema:

**lema:**

Seja $p$ um primo e $a$ e $b$ inteiros. Então

$(a+b)^p \equiv a^p+b^p\pmod{p}$.

**Demonstração:**

$(a+b)^p=(a+b)(a+b)\dots(a+b)$=
$=1.a^p+pa^{p-1}b+C_{2}^pa^{p-2}+C_{2}^pa^{p-3}b³+\dots+C_{p-1}^pa.b^{p-1}+C_{p}^pa^0b^p$

lembrando que $C_{k}^p=\frac{p!}{k!(p-k)!}$

como $C_{k}^p$ é múltiplo de $p$ se $k\ne0$ e $k\ne p$, então

$(a+b)^p=C_{p}^pa^p+C_{p}^pb^p\equiv a^p+b^p \pmod{p}$


**Demonstração PTF:**

Vamos tirar o primo p, e mostrar por indução sobre $a$

caso inicial:

$1^p\equiv1\pmod{p}$.

suponha agora que $m^p\equiv m\pmod{p}$.
vamos mostrar que $(m+1)^p\equiv m+1\pmod{p}$.

$(m+1)^p\equiv m^p+q^p\equiv m+1\pmod{p}$

#### Pequeno teorema de Fermat (Versão 2):

Seja $p$ um primo e $a$ um inteiro não divisível por $p$.

Então

	$a^{p-1}\equiv1\pmod{p}$.

**Exemplo:**

Encontre o resto na divisão de $2^{5432675}$ por $13$ 


$5432675/12=r11,q$

$2^{12}\equiv1\pmod{13}$.
$(2^{12})^{q}.12^{11}\equiv(2^{12})^q.2^{11}$
$\equiv 1.2^{11}\pmod{12}$
