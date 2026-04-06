
### Exemplo:
$$
\int \sin^4(x)dx = \int \left[ \frac{1}{2}(1-\cos(2x)) \right]^2dx
$$
$$
=\frac{1}{4} \int (1-2\cos(2x)+\cos^2(2x))dx
$$
$$
= \frac{1}{4} \int dx - \frac{1}{2} \int \cos(2x)dx+\frac{1}{4}\int \frac{1}{2}(1-\sin(4x))dx
$$
$$
= \frac{x}{4} -\frac{1}{4} \sin(2x)+\frac{x}{8}+\frac{1}{32}\cos(4x)+C
$$


### Exemplo:

$$
\int \tan^6(x)\sec^4(x)dx= \int \tan^6(x)\sec^2(x)\sec^2(x)dx
$$
$$
=\int \tan^6(x)(1+\tan^2(x))\sec^2(x)dx=
$$
$$
u= \tan(x)
$$
$du = \sec^2(x)dx$

$$
\int u^6(1+u^2)du= \int u^6+u^8 du
$$
$$
=\frac{u^7}{7}+\frac{u^9}{9}+C= \frac{\tan^7(x)}{7}+\frac{\tan^9(x)}{9}+C
$$

### Exemplo:

$$
 \int \tan^5x \sec^7xdx
$$
$$
u = \sec x
$$
$$
du = \sec x \tan x
$$
$$
\int \tan^4x \sec^6x\sec x\tan xdx=
$$
$$
\int (\sec^2x-1)^2 \sec^6x \sec x \tan xdx
$$
$$
\int (u^2-1)^2u^6du= \int u^{10}-2u^8+u^6 du
$$

$$
= \frac{u^{11}}{11}-\frac{2u^{9}}{9}+\frac{u^7}{7}+ C= \frac{\sec^{11}x}{11}-\frac{2\sec^{9}x}{9}+\frac{\sec^7x}{7}+C
$$

### Exemplo:

$$
\int tg^3xdx = 
$$

# Substituição Trigonométrica

Para calcular a área um quarto de círculo do raio $u$ , podemos calcular:

$x^2+y^2=r^2$ 
$y^2=r^2-x^2$
$y=\sqrt{ r^2-x^2 }$

$$
\int_{0}^{r} \sqrt{ r^2-x^2 }dx
$$
fazendo a substituição $x=r\sin \theta$ $dx=r\cos \theta d\theta$

$$
\int_{0}^{\pi/2} \sqrt{ r^2-r^2\sin^2\theta } \cdot r\cos \theta d\theta
$$
$$
\int_{0}^{\pi/2} r\sqrt{ 1-\sin^2\theta }\cdot r\cos \theta d\theta
$$
$$
=\int_{0}^{\pi/2} r\cos \theta\cdot r\cos \theta d\theta
$$
$$
= r^2 \int_{0}^{\pi/2} \cos^2\theta d\theta = \frac{r^2}{2} \int_{0}^{\pi/2} [1+\cos(2\theta)]d\theta=
$$
$$
=\frac{r^2}{2}\cdot \left[ \theta+\frac{1}{2} \sin(2\theta) \right]_{0}^{\pi/2}
$$
$$
= \frac{r^2}{2} \frac{\pi}{2}= \frac{\pi r^2}{4}
$$


| Expressão          | Substituição                                                                      | Identidade                      |
| ------------------ | --------------------------------------------------------------------------------- | ------------------------------- |
| $\sqrt{ a^2-x^2 }$ | $x=a\sin \theta, -\frac{\pi}{2}\leq \theta\leq \frac{\pi}{2}$                     | $1-\sin^2=\cos^2\theta$         |
| $\sqrt{ a^2+x^2 }$ | $x=a\tan \theta, -\frac{\pi}{2}< \theta < \frac{\pi}{2}$                          | $1+\tan^2\theta=\sec^2\theta$   |
| $\sqrt{ x^2-a^2 }$ | $x=a\sec \theta, 0\leq \theta< \frac{\pi}{2}$ ou $\pi\leq \theta< \frac{3\pi}{2}$ | $\sec^2\theta-1 = \tan^2\theta$ |
### Exemplo:

$$
\int \frac{\sqrt{ 9-x^2 }}{x^2}dx
$$