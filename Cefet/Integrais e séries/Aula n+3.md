
### Exemplo:

Calcule a área da elipse $\frac{x^2}{9}+\frac{y^2}{4}=1$

$$
\frac{y^2}{4}=1-\frac{x^2}{9} \implies y^2 = \frac{9\cdot4}{9}-\frac{4x^2}{9}
$$
$$
\implies y^2=\frac{4}{9}(9-x^2) \implies y=\frac{2}{3}\sqrt{ 9-x^2 }
$$
$$
\int_{0}^3 \frac{2}{3}\sqrt{ 9-x^2 }dx \implies \frac{2}{3} \int_{0}^3 \sqrt{ 9-x^2 }dx
$$
$$
x = 3sen \theta
$$
$$
dx=3\cos \theta d\theta
$$
$$
= \frac{2}{3} \int_{0}^{\pi/2} \sqrt{ 9-9\sin^2\theta }3\cos \theta d\theta
$$
$$
= \frac{2}{3} \int_{0}^{\pi/2} 3 \cos \theta \cdot 3\cos \theta d\theta = 6 \int_{0}^{\pi/2} \cos^2\theta d\theta
$$
$$
= 6 \int_{0}^{\pi/2} \left( \frac{1}{2} + \frac{\cos(2\theta)}{2} \right)d\theta
$$
$$
= 6 \left[ \frac{\theta}{2} + \frac{\sin(2\theta)}{4} \right]_{0}^{\pi/2} = 6 \frac{\pi}{4}
$$

Logo, a área da elipse é:

$$
4 \cdot \frac{6\pi}{4}= \boxed{6\pi}
$$
#### Exercício:

calcule a área da elipse $\frac{x^2}{a^2}+\frac{y^2}{b^2}=1$.

### Exemplo:

$$
\int \frac{1}{x^2\sqrt{ x^2+4 }}dx
$$
$$
x = a \tan \theta
$$
$$
dx= a \sec^2 \theta
$$
#### Teorema fundamental da álgebra

Dado um polinômio $p(x)=a_{n}x^n+a_{n-1}x^{n-1}+\dots+a_{1}x+a_{0}$, com raízes reais $r_{1},r_{2},\dots,r_{k}$ , $p(x)$ pode ser escrito como $p(x)=a_{n}(x-r^1)(x-r_{2})\dots(x-r_{k})(x^2+b_{1}x+c_{1})\dots(x^2+b_{q}x+c_{q})$ onde $x^2+b_{i}x+c_{i}$ tem raízes complexas.