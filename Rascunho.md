Perfeito — arrumei **tudo pra você**: indentação, blocos de código, matemática em `$$`, pequenos ajustes conceituais e deixei com **cara de trabalho top**. Só copiar pro Obsidian 👇

---

## **3.5.3 Ataque de Wiener (Expoente Privado Pequeno)**

O ataque de Wiener (1990) explora situações em que o expoente privado (d) é pequeno, especificamente quando:

$$  
d < \frac{1}{3} n^{1/4}  
$$

Nesses casos, é possível recuperar (d) a partir da chave pública ((e, n)) utilizando aproximações racionais obtidas por frações contínuas da razão:

$$  
\frac{e}{n}  
$$

O ataque baseia-se na relação:

$$  
ed \equiv 1 \pmod{\varphi(n)}  
$$

Essa relação implica que a fração (\frac{e}{n}) pode ser bem aproximada por frações da forma:

$$  
\frac{k}{d}  
$$

Assim, ao expandir $\frac{e}{n}$ em fração contínua e analisar seus convergentes, é possível recuperar o valor de $d$.

Trata-se de um ataque clássico e documentado, evidenciando que a escolha de um expoente privado pequeno, embora possa melhorar a eficiência da decifragem, compromete severamente a segurança do sistema RSA.

---

### **Código Python – Ataque de Wiener via Frações Contínuas**

```python
from math import isqrt

def fracao_continua(n, d):
    """Gera os coeficientes da expansão em fração contínua de n/d."""
    coefs = []
    while d:
        coefs.append(n // d)
        n, d = d, n % d
    return coefs


def convergentes(coefs):
    """Calcula os convergentes da fração contínua."""
    convs = []

    for i in range(len(coefs)):
        if i == 0:
            convs.append((coefs[0], 1))
        elif i == 1:
            p = coefs[1] * coefs[0] + 1
            q = coefs[1]
            convs.append((p, q))
        else:
            p_prev, q_prev = convs[i - 1]
            p_pprev, q_pprev = convs[i - 2]

            p = coefs[i] * p_prev + p_pprev
            q = coefs[i] * q_prev + q_pprev

            convs.append((p, q))

    return convs


def ataque_wiener(e, n):
    """
    Ataque de Wiener: recupera d quando d é pequeno.
    """

    coefs = fracao_continua(e, n)
    convs = convergentes(coefs)

    for k, d in convs:
        if k == 0:
            continue

        if (e * d - 1) % k != 0:
            continue

        phi = (e * d - 1) // k

        # Resolver x^2 - (n - phi + 1)x + n = 0
        b = n - phi + 1
        discriminante = b * b - 4 * n

        if discriminante < 0:
            continue

        raiz = isqrt(discriminante)

        if raiz * raiz == discriminante:
            p = (b + raiz) // 2
            q = (b - raiz) // 2

            if p * q == n:
                print("Ataque de Wiener bem-sucedido!")
                print(f"d recuperado = {d}")
                print(f"p = {p}, q = {q}")
                return d

    print("Ataque de Wiener falhou.")
    return None
```

---

### **Exemplo de uso (caso vulnerável)**

```python
# Parâmetros vulneráveis
p = 9539
q = 9749
n = p * q

phi_n = (p - 1) * (q - 1)

d = 53  # propositalmente pequeno (vulnerável!)
e = pow(d, -1, phi_n)

print(f'RSA configurado: n={n}, e={e}, d={d}')

# Ataque
d_rec = ataque_wiener(e, n)

# Verificação
M = 42
C = pow(M, e, n)

if d_rec:
    M_dec = pow(C, d_rec, n)
    print(f'Mensagem original: {M} | Decifrado: {M_dec}')
```

---

###  Observação de segurança

O ataque de Wiener demonstra que nunca se deve escolher (d) pequeno como forma de otimização. Na prática, garante-se que (d) seja suficientemente grande para evitar esse tipo de ataque.

---

## **3.5.4 Ataque de Håstad (Broadcast Attack – Expoente Público Pequeno)**

O ataque de Håstad ocorre quando a mesma mensagem (M) é cifrada para múltiplos destinatários usando o mesmo expoente público pequeno (tipicamente ($e = 3$)).

Se tivermos:

$$  
C_i = M^e \mod n_i  
$$

e os módulos ($n_i$) forem coprimos entre si, então é possível reconstruir:

$$  
M^e  
$$

utilizando o Teorema Chinês do Resto. Em seguida, calcula-se a raiz (e)-ésima inteira para recuperar (M).

---

### **Código Python – Ataque de Håstad com CRT**

```python
from sympy import integer_nthroot

def crt(residuos, modulos):
    """Teorema Chinês do Resto"""
    M = 1
    for m in modulos:
        M *= m

    x = 0
    for r, m in zip(residuos, modulos):
        Mi = M // m
        inv = pow(Mi, -1, m)
        x += r * Mi * inv

    return x % M


def ataque_hastad(cifrados, modulos, e=3):
    """Ataque de Håstad"""
    M_e = crt(cifrados, modulos)

    M, exato = integer_nthroot(M_e, e)

    if exato:
        print("Ataque de Håstad bem-sucedido!")
        print(f"Mensagem recuperada: {M}")
        return M
    else:
        print("Ataque falhou (possível uso de padding).")
        return None
```

---

### **Exemplo de uso**

```python
e = 3
M = 42

pares = [(61, 53), (67, 71), (79, 83)]
ns = [p * q for p, q in pares]

cifrados = [pow(M, e, n) for n in ns]

M_rec = ataque_hastad(cifrados, ns, e)

print(f'Mensagem original: {M}')
print(f'Mensagem recuperada: {M_rec}')
```

---

### Defesa

A defesa contra esse ataque é o uso de padding aleatório, como o **OAEP**, que impede que mensagens iguais resultem no mesmo valor cifrado.

---

## **3.6 Pontos Fracos e Análise Crítica**

A análise dos ataques permite identificar vulnerabilidades importantes do RSA quando mal implementado:

- **Primos próximos** → vulneráveis ao método de Fermat
    
- **Expoente privado pequeno** → vulnerável ao ataque de Wiener
    
- **Reutilização de mensagem sem padding** → vulnerável ao ataque de Håstad
    
- **Ataques de temporização** → exploram variações de tempo na execução
    
- **Computação quântica** → algoritmo de Shor compromete o RSA no futuro
    

---

###  Boas práticas

- Escolher (p) e (q) com mesma magnitude, mas não próximos
    
- Garantir (d) suficientemente grande
    
- Utilizar padding seguro (OAEP)
    
- Implementar operações em tempo constante
    
- Considerar criptografia pós-quântica para longo prazo
    
