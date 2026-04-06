## Propriedades da Integral definida:

Ao compararmos 

$\int_{a}^b f(x)dx$ e $\int_{b}^a f(x)dx$,

a única diferença é que trocamos o $\frac{b-a}{m}$ por $\frac{a-b}{m}= -\left( \frac{b-a}{m} \right)$ em cada parcela do somatório, e portanto

$$
\int_{b}^a f(x)dx = - \int_{a}^b f(x)dx
$$
e, consequentemente, 

$$
\int_{a}^a f(x)dx = 0
$$
### Propriedades:

1) $\int_{a}^b c$  $dx = c\cdot(b-a)$ , onde $c$ é constante.
   
2) $\int_{a}^b[f(x)+g(x)]dx=\int_{a}^b f(x) +\int_{a}^bg(x)$
   
3) $\int_{a}^b cf(x)dx= c\int_{a}^b f(x)dx$, onde $c$ é constante.
   
4) $\int_{a}^b [f(x)-g(x)]dx = \int_{a}^b f(x)- \int_{a}^b g(x)$

**Exemplo:**

Usando que $\int_{0}^1 x^2dx=\frac{1}{3}$, calcule $\int_{0}^1(4+3x^2)dx$

$$
\int_{0}^1(4+3x^2)dx = \int_{0}^1 4dx+\int_{0}^1 3x^2dx=
$$
$$
=4\cdot(1-0)+3\int_{0}^1x^2dx=
$$
$$
4+3\cdot \frac{1}{3}= \boxed{5}
$$

5) $\int_{a}^c f(x)dx= \int_{a}^b f(x)dx+ \int_{b}^cf(x)dx$
   
6) Se $f(x)\geq 0$ para $a\leq x\leq b$, então, $\int_{a}^b f(x)dx \geq 0$
   
7) Se $f(x)\geq g(x)$ para $a\leq x\leq b$, então,
	   $$
\int_{a}^b f(x)dx \geq \int_{a}^bg(x)dx
$$
8) Se $m\leq f(x)\leq M$ para $a\leq x\leq b$, então
$$
m(b-a)\leq \int_{a}^b f(x)dx \leq M(b-a)
$$

**Exemplo:**

$f(x)= 3x-2$

$$
2=1\cdot(3-1) \leq\int_{1}^3 (3x-2)dx \leq 7(3-1)=14
$$


## Teorema Fundamental do Cálculo

Dada uma função $f(x)$, vamos tentar calcular

$$
g(x)=\int_{a}^x f(t)dt
$$

Se $f(x) \geq0$ para todo $x$ então $g(x)=\int_{a}^xf(t)dt$ é a área sob a curva entre $a$ e $x$

![[Exemplo 1 Aula 2|1000]]

$g(x+h)-g(x)$ é aproximadamente $h\cdot f(x)$

$g(x+h)-g(x) \approx h\cdot f(x)$

$\frac{g(x+h)-g(x)}{h} \approx f(x)$

Quando $h$ é pequeno

$$
\lim_{ h \to 0 } \frac{g(x+h)-g(x)}{h} = f(x)
$$

ou seja,

$$
g'(x)=f(x)
$$

### Teorema Fundamental do Calculo (Versão 1)

Se $f$ é contínua em $[a,b]$ então a função g definida por $g(x)=\int_{a}^x f(t)dt$ para $a\leq x\leq b$ é continuo e $[a,b]$, derivável em $(a,b)$, e $g'(x)=f(x)$

#### Exemplo:

$$
\int_{0}^xt^2dt = \frac{x^3}{3}
$$
$$
\int_{1}^x t^2 dt= \frac{x^3}{3}-\frac{1}{3}
$$

### Teorema Fundamental do Calculo (Versão 2)

Se $ f$ é contínua em $[a,b]$,então

$$
\int_{a}^b f(x)dx=F(b)-F(a)
$$
onde $F(x)$ é qualquer função tal que $F'(x)=f(x)$.

Se $F(x)$ é tal que $F'(x)=f(x)$, dizemos que $F(x)$ é uma <u>primitiva</u> de $f(x)$.

#### <u>Demonstração</u>:

Seja $g(x)=\int_{0}^x f(t)dt$. Pela versão 1, $g'(x)=f(x)$.

Se $F(x)$ é uma primitiva de $f(x)$, então $F'(x)=f(x)$
Como $F'(x)=g'(x)$, então $F(x)=g(x)+C$.

Logo

$$
F(b)-F(a)=(g(b)+C)-(g(a)+C)=
$$
$$
=g(b)+(-g(a)-C)=g(b)-g(a)
$$
$$
=\int_{a}^b f(t)dt  -\int_{a}^a f(t)dt= \int_{a}^b f(x)dx 
$$
$$
\blacksquare 
$$
