
Ao calcular a derivada de um produto, obtemos 

$[f(x)\cdot g(x)]'=f'(x)\cdot g(x)+f(x)\cdot g'(x)$

$[uv]'=u'v+uv'$

$uv'=[uv']-u'v$

integrando,

$\int uv'dx=uv-\int u'vdx$
$\boxed{\int udv=uv-\int vdu}$


#### Exemplo:

Calcule $\int xsen(x)dx$

$u=x$                 $dv=sen(x)dx$
$du=dx$             $v= -\cos(x)$

$$
\int x \sin xdx=-x\cos x-\int-\cos xdx
$$
$$
\int-x\cos x+\int \cos x dx=-\cos x+\sin x+C
$$


$u=sen(x)$       $dv=xdx$
$du= \cos xdx$   $v=\frac{x^2}{2}$

$$
\frac{x^2}{2} \sin x- \int \frac{x^2}{2} \cos xdx
$$


> [!NOTE] É mais dificil 
$u=sen(x)$       $dv=xdx$
$du= \cos xdx$   $v=\frac{x^2}{2}$
>$$
\frac{x^2}{2} \sin x- \int \frac{x^2}{2} \cos xdx
$$


### Exemplo:

Calcule $\int xe^xdx$

$u=x$                       $dv=e^x dx$
$du=dx$                  $v=e^x$

$$
\int xe^xdx=xe^x-\int e^xdx=xe^x-e^x+C
$$

### Exemplo:

Calcule $\int x^2e^xdx$

$u = x^2$                        $dv=e^x dx$
$du= 2xdx$                 $v= e^x$


$$
\int x^2e^xdx = x^2e^x-2\int xe^xdx= x^2e^x-2xe^x-\int e^xdx
$$
$$
= x^2-e^x-2xe^x+2e^x+C
$$

### Exemplo:

Calcule $\int \ln xdx$

$u= \ln x$         $dv=dx$
$du=\frac{1}{x}dx$     $v=x$
$$
\int \ln xdx=x\ln x-\int x \frac{1}{x}dx= x\ln x-\int dx
$$
$$
= x\ln x-x+C
$$


# Integrais Trigonométricas

### Exemplo:

$$
\int \cos^3 x dx= \int \cos x\cdot \cos^2xdx=
$$
$$
=\int \cos x (1-\sin^2 x)dx
$$

$$
u=\sin x, du=\cos xdx
$$
$$
=\int(1-u^2)du = u - \frac{u^3}{3}+C=
$$
$$
\int \sin x - \frac{\sin^3x}{3} +C
$$

#### Solução alternativa:

$$
\int \cos^3dx = \int \cos x\cdot \cos^2dx=
$$
$$
u = \cos^2x, dv=\cos xdx
$$
$$
du = -2\cos x\sin xdx,v=\sin x
$$

$$
\cos^2x\sin x-2\int- \sin^2 x \cos xdx
$$








