**Centro Federal de Educação Tecnológica de Minas Gerais**
Tópicos Especiais de Matemática: Criptografia

# **Estudo da Eficiência e Algoritmos de Ataque ao RSA**

Aluno: Gabriel Augusto de Lima Maia
Curso: Engenharia da Computação
Belo Horizonte – MG, 2026

  

# **1. Objetivo**

Este trabalho tem por objetivo apresentar uma análise aprofundada da Criptografia RSA (Rivest–Shamir–Adleman), explorando seus fundamentos matemáticos, assinaturas digitais, variantes do algoritmo, métricas de eficiência e, sobretudo, os principais algoritmos de ataque conhecidos na literatura. A análise é conduzida à luz da Teoria dos Números, disciplina que fornece as bases teóricas indispensáveis para a compreensão e a avaliação crítica do RSA. Por meio de exemplos práticos implementados em Python, busca-se tornar concreto o entendimento dos pontos fortes e das vulnerabilidades do algoritmo, contribuindo para a formação do raciocínio criptográfico no contexto da engenharia de computação.

  
  

# **2. Declaração de Uso de IA**

Este trabalho foi elaborado com o auxílio de Inteligência Artificial (IA) como ferramenta de suporte à pesquisa, organização de conteúdo e revisão textual. Todo o conteúdo foi revisado, compreendido e validado pelo(a) autor(a), assumindo plena responsabilidade intelectual pelo material apresentado. A IA foi utilizada como ferramenta complementar, não substituindo o estudo, a análise crítica e o entendimento dos conceitos expostos.

# **3. Desenvolvimento**

## **3.1 Fundamentos Matemáticos do RSA**

O algoritmo RSA, proposto em 1977 por Ron Rivest, Adi Shamir e Leonard Adleman, baseia-se em conceitos fundamentais da Teoria dos Números, especialmente aqueles relacionados à aritmética modular e propriedades dos números primos.

### **Números primos e fatoração**

Um número primo é aquele que possui exatamente dois divisores positivos distintos: 1 e ele mesmo. A segurança do RSA depende da dificuldade de fatorar um número inteiro grande n em seus fatores primos p e q, problema conhecido como **fatoração de inteiros**. Embora a multiplicação de primos seja computacionalmente simples, o processo inverso é considerado difícil para números suficientemente grandes.

### **Aritmética modular**
  

A aritmética modular é a base operacional do RSA. Dizemos que:
  $$a\equiv b \mod n$$
 
quando n divide $(a−b)$. Essa estrutura permite trabalhar com números dentro de um sistema cíclico, essencial para operações de criptografia.

### **Máximo divisor comum e números coprimos**  
  
Dois números inteiros são ditos coprimos quando seu máximo divisor comum (mdc) é igual a $1$. No RSA, a escolha do expoente público e exige que:

$$mdc(e,φ(n))=1$$

Essa condição garante a existência do inverso modular de $e$.

### **Função totiente de Euler**
  

A função totiente $φ(n)$ conta quantos inteiros positivos menores que $n$ são coprimos com ele. Para $n=p⋅q$, com $p$ e $q$ primos distintos:

$φ(n)=(p−1)(q−1)$

Essa função é essencial para a construção da chave privada.

### **Inverso modular**

O inverso modular de um número e módulo $φ(n)$ é um número $d$ tal que:

  $e⋅d\equiv 1 \mod {φ(n)}$

Esse valor $d$ pode ser encontrado utilizando o algoritmo de Euclides estendido, sendo fundamental para a decifragem no RSA.

### **Teorema de Euler**
  
O funcionamento do RSA é garantido pelo **Teorema de Euler**, que afirma que, para qualquer inteiro a coprimo com n:

  $a^{φ(n)}\equiv1\mod n$

Esse resultado assegura que a operação de criptografia e descriptografia são inversas entre si.

O Teorema de Euler é uma generalização do **Pequeno Teorema de Fermat**, que afirma que, se $p$ é primo e $a$ não é múltiplo de $p$, então $a^{p−1}\equiv1 \mod p$. Esse resultado é fundamental para a construção de sistemas criptográficos baseados em congruências modulares.

### Aplicação no RSA

A partir desses conceitos, o RSA define:

- Chave pública: $(n,e)$
- Chave privada: $d$

A cifragem de uma mensagem $M$ é dada por:

$$C=M^e \mod n$$

e a decifragem por:

$$M=C^d \mod n$$

A validade dessas operações decorre diretamente das propriedades da aritmética modular e do Teorema de Euler.

Exemplo de código:

```python
# =========================
# Parâmetros RSA (didáticos)
# =========================
p = 61
q = 53
n = p * q # 3233
phi = (p - 1)*(q - 1)
  
e = 17

# Inverso modular (já calculado)

d = 2753

# =========================
# Funções RSA
# =========================

def criptografar_bytes(texto, e, n):
	dados = texto.encode("utf-8")
	cifrado = [] 
	
	for byte in dados:
		c = pow(byte, e, n)
		cifrado.append(c)
		
	return cifrado


def descriptografar_bytes(cifrado, d, n):
	bytes_recuperados = []

	for c in cifrado:
		m = pow(c, d, n)
		bytes_recuperados.append(m)
	
	return bytes(bytes_recuperados).decode("utf-8")

  

# # =========================
# # Teste com UTF-8
# # =========================
mensagem = "Olá mundo!"

cifrado = criptografar_bytes(mensagem, e, n)
decifrado = descriptografar_bytes(cifrado, d, n)

print("Mensagem:", mensagem)
print("Cifrado:", cifrado)
print("Decifrado:", decifrado)
```
Saída:

```
Mensagem: Olá mundo!
Cifrado: [1307, 745, 205, 2017, 1992, 2271, 2160, 2235, 1773, 2185, 1853]
Decifrado: Olá mundo!
```

Foi usado UTF-8, para a representação de todos os caracteres do alfabeto e seus acentos, realizando a cifragem em nível de byte, que garante que cada valor numérico seja menor que o módulo $n$, evitando a perda de informação

## **3.2 Assinaturas Digitais com RSA**

O RSA também é amplamente utilizado em esquemas de assinatura digital, garantindo autenticidade e integridade das mensagens. Diferentemente da cifragem, o processo de assinatura utiliza a chave privada do emissor.

Na prática, não se assina diretamente a mensagem $M$, mas sim um resumo criptográfico (hash) da mensagem. Assim, a assinatura é calculada como:

$S=H(M)^d \pmod  n$

onde $H(M)$ é o hash da mensagem.

Para verificar a assinatura, o receptor utiliza a chave pública do remetente e calcula:

$M'=S^e \pmod  n$

A assinatura é considerada válida se:

$M'=H(M)$

Esse mecanismo garante que a mensagem não foi alterada (integridade) e que foi realmente enviada pelo detentor da chave privada (autenticidade).

Os principais padrões de assinatura digital baseados em RSA incluem o RSA-PKCS#1 v1.5 e o RSA-PSS (Probabilistic Signature Scheme), sendo este último considerado mais seguro por incorporar aleatoriedade no processo de assinatura. 
## **3.3 Variantes do RSA**

Com o tempo, diversas variantes foram desenvolvidas para aumentar a eficiência ou a segurança do RSA original:

- Multi-Prime RSA: utiliza três ou mais primos $(p, q, r, ...)$ para construir $n$, tornando a exponenciação modular mais rápida via Teorema Chinês do Resto (CRT).
    
- RSA-CRT: aplica o Teorema Chinês do Resto para acelerar a decifragem em até 4 vezes.
    
- RSA com expoente público pequeno ($e = 65537$): acelera a cifragem, mas requer cuidados para evitar ataques.
    
- OAEP (Optimal Asymmetric Encryption Padding): esquema de padding que adiciona aleatoriedade ao processo de cifragem, protegendo contra ataques de texto cifrado escolhido.
    

  
  

## **3.4 Análise de Eficiência do RSA**

A principal vantagem do RSA reside em sua fundamentação matemática sólida, baseada na dificuldade computacional da fatoração de inteiros grandes. No entanto, seu custo computacional é significativamente superior ao de algoritmos simétricos, como o AES, o que impacta diretamente sua aplicação prática.

A eficiência do RSA está relacionada principalmente às operações de exponenciação modular com números inteiros de grande tamanho. As principais etapas apresentam as seguintes características:

- **Geração de chaves:** envolve a geração de números primos grandes e a verificação de primalidade, geralmente realizada por algoritmos probabilísticos como o teste de Miller-Rabin. Esse processo possui custo computacional elevado, mas é executado com pouca frequência.
- **Cifragem:** apresenta custo relativamente baixo quando o expoente público $e$ é pequeno (como $e=65537$), sendo aproximadamente da ordem de$O((\log n)^2)$. Isso torna a operação de cifragem eficiente na prática.
- **Decifragem:** é computacionalmente mais custosa, pois utiliza um expoente privado $d$ significativamente maior, resultando em complexidade aproximada de $O((\log n)^3)$. Entretanto, essa operação pode ser otimizada por meio do uso do Teorema Chinês do Resto (CRT), reduzindo consideravelmente o tempo de execução.

Na prática, a exponenciação modular é implementada com algoritmos eficientes, como o método _square-and-multiply_, que permite calcular potências de forma rápida mesmo com inteiros grandes.

Devido ao seu custo computacional, o RSA não é utilizado para cifrar grandes volumes de dados. Em vez disso, é empregado em esquemas híbridos de criptografia, nos quais o RSA é utilizado para cifrar chaves de sessão, enquanto algoritmos simétricos, como o AES, são responsáveis pela cifragem dos dados propriamente ditos.

Atualmente, tamanhos de chave de 2048 bits são considerados padrão para aplicações seguras, enquanto chaves de 4096 bits oferecem maior margem de segurança para aplicações de longo prazo, ao custo de maior processamento.
  
  

## **3.5 Algoritmos de Ataque ao RSA**

A seguir apresentamos os principais algoritmos de ataque ao RSA, com análise teórica e implementação prática em Python. Os exemplos utilizam valores pequenos para fins didáticos — em implementações reais, os primos são centenas de dígitos maiores.

  
  

## **3.5.1 Ataque por Fatoração por Força Bruta**

O ataque mais direto ao RSA é tentar fatorar n encontrando p e q. Para n pequeno, a força bruta é viável. Para n de 2048 bits, o melhor algoritmo clássico (General Number Field Sieve) levaria tempo astronomicamente longo.

  
  

**Código Python – Fatoração por Força Bruta:**

```python
import math

def fatoracao_forca_bruta(n):

"""Tenta encontrar p e q fatorando n por força bruta."""

	for p in range(2, int(math.isqrt(n)) + 1):
		if n % p == 0:
			q = n // p
			print(f'n = {n} fatorado: p = {p}, q = {q}')
	return p, q

return None
```

  

# Exemplo com n pequeno (vulnerável)

```python
n = 3233 # p=61, q=53

e = 17

p, q = fatoracao_forca_bruta(n)

phi_n = (p - 1) * (q - 1)

d = pow(e, -1, phi_n) # Chave privada recuperada

print(f'Chave privada recuperada: d = {d}')
```

Saída:

```
n = 3233 fatorado: p = 53, q = 61
Chave privada recuperada: d = 2753
```
  

## **3.5.2 Fatoração de Fermat**

O método de Fermat baseia-se na representação de um número inteiro nnn como diferença de quadrados:

$n = a^2 - b^2 = (a - b)(a + b)$

Para um número composto $n=p\cdot q$, com $p$ e $q$ primos ímpares, é possível escrever:

$$
a=\frac{p+q}{2}, b=\frac{p-q}{2}
$$

Dessa forma, a fatoração de $n$ pode ser obtida ao encontrar valores inteiros $a$ e $b$ tais que $a^2 - n = b^2$. O método é particularmente eficiente quando os fatores $p$ e $q$ são próximos, pois nesse caso o valor de $b$ é pequeno, reduzindo o número de iterações necessárias para encontrar a solução.

**Código Python – Fatoração de Fermat:**

```python
import math

def fatoracao_fermat(n):
    """
    Fatoração de Fermat: eficiente quando p e q são próximos.
    Explora n = a^2 - b^2 = (a+b)(a-b)
    """

    a = math.isqrt(n)

    if a * a < n:
        a += 1  # Garante que a^2 >= n

    while True:
        b2 = a * a - n
        b = math.isqrt(b2)

        if b * b == b2:  # b é quadrado perfeito
            p = a - b
            q = a + b

            print(f'Fermat: a={a}, b={b}')
            print(f'Fatores encontrados: p={p}, q={q}')

            return p, q

        a += 1

```
  

# Exemplo: primos próximos (vulnerável ao método de Fermat)

```python
p = 9999991

q = 9999973

n = p * q

print(f'n = {n}')

p_rec, q_rec = fatoracao_fermat(n_f)

# Verificação (independente da ordem)
if set([p_rec, q_rec]) == set([p_f, q_f]):
	print("Resultado: fatoração correta ✅")
else:
	print("Resultado: fatoração incorreta ❌")
```
Saída:

```
n = 99999640000243
Fermat: a=9999982, b=9
Fatores encontrados: p=9999973, q=9999991
Resultado: fatoração correta ✅
```
  

Este ataque ressalta a importância de escolher primos $p$ e $q$ com diferença suficientemente grande. O método de Fermat é particularmente eficiente quando os fatores são próximos entre si, pois o valor $b = \frac{p - q}{2}$​ torna-se pequeno, reduzindo o número de iterações necessárias. Portanto, na prática, recomenda-se que $p$ e $q$ sejam escolhidos de forma aleatória e com magnitude semelhante, mas sem proximidade excessiva, evitando vulnerabilidades a esse tipo de ataque.

  
  

## **3.5.3 Ataque de Wiener (Expoente Privado Pequeno)**

O ataque de Wiener (1990) explora situações em que o expoente privado $d$ é pequeno, especificamente quando:

$$  
d < \frac{1}{3} n^{1/4}  
$$

Nesses casos, é possível recuperar $d$ a partir da chave pública $(e, n)$ utilizando aproximações racionais obtidas por frações contínuas da razão:

$$  
\frac{e}{n}  
$$

O ataque baseia-se na relação:

$$  
ed \equiv 1 \pmod{\varphi(n)}  
$$

Essa relação implica que a fração $\frac{e}{n}$ pode ser bem aproximada por frações da forma:

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

O ataque de Wiener demonstra que nunca se deve escolher $d$ pequeno como forma de otimização. Na prática, garante-se que $d$ seja suficientemente grande para evitar esse tipo de ataque.

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

utilizando o Teorema Chinês do Resto. Em seguida, calcula-se a raiz $e$-ésima inteira para recuperar ($M$).

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
# **4. Conclusão**

O RSA é um algoritmo de enorme importância histórica e prática para a criptografia moderna, servindo de base para protocolos como TLS/SSL, PGP e SSH. Sua segurança reside na dificuldade computacional da fatoração de inteiros grandes, sustentada por séculos de Teoria dos Números.

A análise dos algoritmos de ataque — fatoração por força bruta, método de Fermat, ataque de Wiener e ataque de Håstad — revela que a segurança do RSA depende criticamente das escolhas feitas na geração de chaves e no uso de padding adequado. Implementações ingênuas ou com parâmetros fracos são vulneráveis a ataques matemáticos bem estabelecidos.

Os experimentos em Python demonstraram, de forma concreta, como cada vulnerabilidade pode ser explorada em cenários didáticos, reforçando a importância da engenharia criptográfica responsável. A compreensão desses ataques é fundamental para que engenheiros de computação possam avaliar criticamente sistemas criptográficos e adotar melhores práticas de implementação.

Como perspectiva futura, destaca-se o desafio da transição para a criptografia pós-quântica, motivada pela ameaça do algoritmo de Shor em computadores quânticos. Algoritmos como o CRYSTALS-Kyber e o CRYSTALS-Dilithium, padronizados pelo NIST em 2024, representam a nova fronteira da segurança criptográfica. O estudo do RSA, portanto, não é apenas uma análise de um algoritmo legado, mas uma introdução essencial ao raciocínio matemático que norteia o design de qualquer sistema criptográfico seguro.

Esta primeira etapa da disciplina de Criptografia contribuiu significativamente para consolidar a visão de que segurança computacional é tanto matemática quanto engenharia — exigindo rigor teórico e consciência das limitações práticas de cada solução adotada.

  
  

# **5. Referências**

RIVEST, R. L.; SHAMIR, A.; ADLEMAN, L. A Method for Obtaining Digital Signatures and Public-Key Cryptosystems. Communications of the ACM, v. 21, n. 2, p. 120–126, 1978.

WIENER, M. J. Cryptanalysis of Short RSA Secret Exponents. IEEE Transactions on Information Theory, v. 36, n. 3, p. 553–558, 1990.

HÅSTAD, J. Solving Simultaneous Modular Equations of Low Degree. SIAM Journal on Computing, v. 17, n. 2, p. 336–341, 1988.

STALLINGS, W. Cryptography and Network Security: Principles and Practice. 7. ed. Pearson, 2017.

BONEH, D. Twenty Years of Attacks on the RSA Cryptosystem. Notices of the American Mathematical Society, v. 46, n. 2, p. 203–213, 1999.

NIST. Post-Quantum Cryptography Standardization. Disponível em: https://csrc.nist.gov/projects/post-quantum-cryptography. Acesso em: 2025.

PYTHON SOFTWARE FOUNDATION. Python 3 Documentation. Disponível em: https://docs.python.org. Acesso em: 2025.