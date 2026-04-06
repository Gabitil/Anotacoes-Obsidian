
### Definição:

**a)** Se $f$ é continua em $[a,b)$ e descontinua em $b$, então

$$
\int_{a}^b f(x)dx = \lim_{ t \to b⁻ } \int_{a}^t f(x)dx 
$$
se o limite existir.

**b)** Se $f$ é continua em $(a,b]$ e descontinua em a, então
$$
\int_{a}^b f(x)dx = \lim_{ t \to a⁺ } \int_{t}^b f(x)dx 
$$
se o limite existir.

A integral imprópria $\int_{a}^b f(x)dx$ é dita convergente se o limite existir, e divergente caso contrário
**c)** Se $f$ tiver uma descontinuidade em $c$, onde $a<c<b$, e ambas as integrais $\int_{a}^c f(x)dx$ e $\int_{c}^b f(x)dx$ são convergentes, então definimos

$$
\int_{a}^b f(x)dx = \int_{a}^c f(x)dx + \int_{c}^b f(x)dx
$$
### Exemplo:

calcule:

$$
\int_{2}^5 \frac{1}{\sqrt{ x-2 }}dx
$$
$$
\lim_{ t \to 2^+ } \int_{t}^5\frac{1}{\sqrt{ x-2 }}dx  
$$
$$
u = x-2
$$
$$
du = dx
$$
$\int \frac{1}{\sqrt{ u }}du =\int u^{-\frac{1}{2}}du= \frac{u^{\frac{1}{2}}}{\frac{1}{2}}+C= 2\sqrt{ u}+C$

$$
= \lim_{ t \to 2^+ } [2\sqrt{ x-2 }]_{t}^5 = \lim_{ t \to 2⁺ } (2\sqrt{ 3 }-2\sqrt{ t-2 })=2 \sqrt{ 3 }- 0= \boxed{2\sqrt{ 3 }}  
$$
### Teorema da comparação

Sejam $f$ e $g$ funções contínuas com $f(x)\geq g(x) \geq 0$ para todo $x\geq a$.
**a)** se