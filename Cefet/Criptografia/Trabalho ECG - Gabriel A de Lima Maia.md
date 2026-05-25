#### Centro Federal de Educação Tecnológica de Minas Gerais

Tópicos Especiais de Matemática: Criptografia

# **Estudo da Eficiência e Algoritmos de Ataque ao ECC**

Aluno: Gabriel Augusto de Lima Maia  
Curso: Engenharia da Computação  
Belo Horizonte – MG, 2026

---

# **1. Objetivo**

Este trabalho tem como objetivo apresentar uma análise da Criptografia de Curvas Elípticas (_Elliptic Curve Cryptography_ – ECC), explorando seus fundamentos matemáticos, aplicações práticas, eficiência computacional e principais algoritmos de ataque.

A abordagem será conduzida sob a perspectiva da Engenharia da Computação, buscando compreender o funcionamento do ECC de maneira aplicada e intuitiva, sem aprofundamento excessivo em demonstrações matemáticas formais.

Além da fundamentação teórica, o trabalho também apresenta exemplos práticos implementados em Python, permitindo visualizar como operações envolvendo curvas elípticas são utilizadas na geração de chaves criptográficas e na segurança de protocolos modernos.

Por fim, será realizada uma análise crítica dos pontos fortes e limitações do ECC, incluindo ataques clássicos ao problema do logaritmo discreto elíptico e a ameaça futura da computação quântica.

---

# **2. Declaração de Uso de IA**

Este trabalho foi elaborado com o auxílio de Inteligência Artificial (IA) como ferramenta de suporte à pesquisa, organização de conteúdo, revisão textual e auxílio didático na compreensão dos conceitos matemáticos e computacionais relacionados à Criptografia de Curvas Elípticas.

Todo o conteúdo foi revisado, compreendido e validado pelo autor, que assume total responsabilidade intelectual pelas informações apresentadas.

A IA foi utilizada exclusivamente como ferramenta complementar ao estudo, não substituindo o processo de aprendizagem, interpretação crítica e desenvolvimento do trabalho.

---

# **3. Desenvolvimento**

# **3.1 Fundamentação Matemática do ECC**

A Criptografia de Curvas Elípticas (ECC) é um sistema criptográfico assimétrico baseado em propriedades matemáticas de curvas algébricas definidas sobre corpos finitos.

Diferentemente do RSA, cuja segurança depende da dificuldade da fatoração de inteiros grandes, o ECC baseia sua segurança na dificuldade computacional do Problema do Logaritmo Discreto em Curvas Elípticas (_Elliptic Curve Discrete Logarithm Problem_ – ECDLP).

Mesmo utilizando chaves significativamente menores, o ECC consegue oferecer níveis de segurança equivalentes ou superiores aos do RSA.

## **3.1.1 Aritmética Modular**

Assim como no RSA, o ECC utiliza operações em aritmética modular.

Dizemos que:

$$  
a \equiv b \pmod p  
$$

quando $a$ e $b$ deixam o mesmo resto na divisão por $p$.

Exemplo:

$$  
29 \equiv 5 \pmod{24}  
$$

pois:

$$  
29 \mod 24 = 5  
$$

No ECC, praticamente todas as operações são realizadas módulo um número primo $p$.

Isso significa que:

- somas
    
- multiplicações
    
- divisões
    
- potências
    

são calculadas dentro de um conjunto finito de valores.

---

## **3.1.2 Corpos Finitos**

O ECC normalmente trabalha sobre corpos finitos denotados por:

$$  
\mathbb{F}_p  
$$

onde $p$ é um número primo.

Isso significa que todos os cálculos são realizados utilizando apenas os números:

$$  
0,1,2,3,\dots,p-1  
$$

Por exemplo, em:

$$  
\mathbb{F}_{17}  
$$

os únicos valores possíveis são:

$$  
0,1,2,\dots,16  
$$

Caso um cálculo ultrapasse esse intervalo, aplica-se a operação módulo $17$.

Exemplo:

$$  
20 \equiv 3 \pmod{17}  
$$

---

## **3.1.3 Curvas Elípticas**

Uma curva elíptica pode ser definida pela equação:

$$  
y^2 = x^3 + ax + b  
$$

Para que a curva seja válida, é necessário que:

$$  
4a^3 + 27b^2 \neq 0  
$$

Essa condição garante que a curva não possua singularidades, como pontos de cruzamento ou cúspides.

Quando utilizada em criptografia, essa equação é calculada módulo um número primo $p$.

Exemplo:

$$  
y^2 \equiv x^3 + 2x + 3 \pmod{97}  
$$

Nesse caso, todos os pontos válidos da curva possuem coordenadas inteiras dentro do conjunto:

$$  
0,1,2,\dots,96  
$$

---

## **3.1.4 Soma de Pontos**

A operação fundamental do ECC é a soma de pontos sobre a curva.

Dados dois pontos:

$$  
P=(x_1,y_1)  
$$

$$  
Q=(x_2,y_2)  
$$

é possível calcular:

$$  
R=P+Q  
$$

Geometricamente, traça-se uma reta entre $P$ e $Q$. Essa reta intersecta a curva em um terceiro ponto. Em seguida, realiza-se uma reflexão em relação ao eixo horizontal para obter o resultado da soma.

No contexto criptográfico, essa operação é adaptada para aritmética modular.

A inclinação da reta é dada por:

$$  
\lambda = \frac{y_2-y_1}{x_2-x_1}  
$$

Entretanto, como não existe divisão direta em aritmética modular, utiliza-se o inverso modular:

$$  
\lambda = (y_2-y_1)(x_2-x_1)^{-1} \pmod p  
$$

A partir disso, calculam-se as coordenadas do novo ponto.

---

## **3.1.5 Multiplicação Escalar**

A principal operação utilizada no ECC é a multiplicação escalar.

Dado um ponto $P$ e um inteiro $k$, define-se:

$$  
Q=kP  
$$

Isso significa:

$$  
Q=P+P+P+\dots+P  
$$

com $P$ sendo somado $k$ vezes.

Essa operação é computacionalmente simples de realizar.

Porém, o processo inverso:

$$  
Q=kP  
$$

Descobrir $k$ conhecendo apenas $P$ e $Q$ é considerado extremamente difícil.

Esse problema é chamado de:

$$  
\text{Problema do Logaritmo Discreto em Curvas Elípticas (ECDLP)}  
$$

A segurança do ECC depende diretamente da dificuldade computacional desse problema.

---

# **3.2 Funcionamento do ECC**

O ECC é um sistema criptográfico assimétrico.

Isso significa que ele utiliza:

- uma chave pública
    
- uma chave privada
    

A chave privada é um número inteiro secreto:

$$  
k  
$$

A chave pública é obtida realizando:

$$  
Q=kP  
$$

onde:

- $P$ é um ponto público da curva
    
- $k$ é a chave privada
    
- $Q$ é a chave pública
    

Embora seja fácil calcular $Q$ a partir de $k$, descobrir $k$ conhecendo apenas $P$ e $Q$ é computacionalmente inviável para curvas suficientemente grandes.

---

## **3.2.1 ECDH – Troca de Chaves**

O algoritmo ECDH (_Elliptic Curve Diffie-Hellman_) é utilizado para troca segura de chaves.

O funcionamento básico ocorre da seguinte forma:

### Alice

Escolhe:

$$  
a  
$$

Calcula:

$$  
A=aP  
$$

### Bob

Escolhe:

$$  
b  
$$

Calcula:

$$  
B=bP  
$$

Depois:

Alice calcula:

$$  
aB  
$$

Bob calcula:

$$  
bA  
$$

Como:

$$  
aB = abP  
$$

$$  
bA = baP  
$$

ambos obtêm a mesma chave secreta.

---

## **3.2.2 Assinaturas Digitais – ECDSA**

O principal esquema de assinatura digital baseado em ECC é o ECDSA (_Elliptic Curve Digital Signature Algorithm_).

Ele é amplamente utilizado em:

- Bitcoin
    
- HTTPS/TLS
    
- SSH
    
- certificados digitais
    
- carteiras de criptomoedas
    

O ECDSA permite:

- autenticação
    
- integridade
    
- não repúdio
    

Na prática, não se assina diretamente a mensagem original.

Primeiramente, aplica-se uma função hash criptográfica, como SHA-256:

$$  
h = H(M)  
$$

A assinatura é então gerada utilizando o hash da mensagem e a chave privada.

Isso reduz o custo computacional e aumenta a segurança.

---

# **3.3 Eficiência do ECC**

Uma das principais vantagens do ECC é sua elevada eficiência criptográfica.

Comparado ao RSA, o ECC consegue oferecer níveis equivalentes de segurança utilizando chaves significativamente menores.

A tabela abaixo apresenta uma comparação aproximada:

|ECC|RSA|
|---|---|
|224 bits|2048 bits|
|256 bits|3072 bits|
|384 bits|7680 bits|

Isso produz diversas vantagens:

- menor consumo de memória
    
- menor uso de processamento
    
- menor largura de banda
    
- maior velocidade
    

Por esse motivo, o ECC é amplamente utilizado em:

- dispositivos móveis
    
- sistemas embarcados
    
- Internet das Coisas (IoT)
    
- criptomoedas
    
- aplicações de alta performance
    

Além disso, operações envolvendo ECC geralmente exigem menor consumo energético quando comparadas ao RSA.

---

# **3.4 Algoritmos de Ataque ao ECC**

A segurança do ECC depende diretamente da dificuldade do Problema do Logaritmo Discreto em Curvas Elípticas.

Apesar disso, existem algoritmos capazes de atacar implementações fracas ou curvas inadequadas.

---

# **3.4.1 Ataque por Força Bruta**

O ataque mais simples consiste em testar sucessivamente:

$$  
P,2P,3P,4P,\dots  
$$

até encontrar:

$$  
Q=kP  
$$

Esse ataque possui complexidade exponencial e torna-se inviável para curvas reais utilizadas em criptografia moderna.

Entretanto, em curvas pequenas utilizadas para fins didáticos, ele pode ser demonstrado computacionalmente.

---

## **Código Python – Ataque por Força Bruta ao ECDLP**

```python
# ==========================================
# ECC Didático - Ataque por força bruta
# ==========================================

# Curva:
# y² = x³ + 2x + 3 mod 97

p = 97
a = 2
b = 3

# Ponto gerador
G = (3, 6)


def inverso_modular(k, p):
    """Calcula inverso modular."""
    return pow(k, -1, p)



def soma_pontos(P, Q):
    """Soma dois pontos na curva elíptica."""

    if P is None:
        return Q

    if Q is None:
        return P

    x1, y1 = P
    x2, y2 = Q

    # P + (-P) = ponto no infinito
    if x1 == x2 and (y1 + y2) % p == 0:
        return None

    # Dobramento
    if P == Q:
        lamb = (3 * x1 * x1 + a) * inverso_modular(2 * y1, p)
    else:
        lamb = (y2 - y1) * inverso_modular(x2 - x1, p)

    lamb %= p

    x3 = (lamb * lamb - x1 - x2) % p
    y3 = (lamb * (x1 - x3) - y1) % p

    return (x3, y3)



def multiplicacao_escalar(k, P):
    """Calcula kP."""

    resultado = None

    for _ in range(k):
        resultado = soma_pontos(resultado, P)

    return resultado


# ==========================================
# Geração de chave
# ==========================================

chave_privada = 15
Q = multiplicacao_escalar(chave_privada, G)

print(f"Chave pública Q = {Q}")


# ==========================================
# Ataque por força bruta
# ==========================================

print("\nIniciando ataque...\n")

for k in range(1, 100):

    tentativa = multiplicacao_escalar(k, G)

    print(f"{k}G = {tentativa}")

    if tentativa == Q:
        print("\nChave privada encontrada!")
        print(f"k = {k}")
        break
```

---

## **Análise do Ataque**

O ataque apresentado demonstra que descobrir a chave privada em curvas pequenas é relativamente simples.

Porém, curvas utilizadas na prática possuem ordens extremamente grandes, normalmente envolvendo números de 256 bits ou superiores.

Nesses casos, a quantidade de operações necessárias torna o ataque por força bruta inviável computacionalmente.

---

# **3.4.2 Baby-Step Giant-Step**

O algoritmo Baby-Step Giant-Step é um método mais eficiente para resolver o Problema do Logaritmo Discreto.

Sua ideia principal consiste em dividir o problema em duas partes:

- baby steps
    
- giant steps
    

Isso reduz significativamente o número de operações necessárias.

A complexidade do algoritmo é aproximadamente:

$$  
O(\sqrt{n})  
$$

onde $n$ representa a ordem do grupo.

Embora seja muito mais eficiente que força bruta, ainda é inviável contra curvas modernas corretamente implementadas.

```python
# ============================================================
#  Baby-Step Giant-Step (BSGS) – Ataque ao ECDLP
#  Curva: y² ≡ x³ + 3x + 6 (mod 97)
# ============================================================
#
#  IDEIA GERAL DO ALGORITMO
#  -------------------------
#  Queremos encontrar k tal que Q = kG (o "logaritmo discreto").
#
#  Em vez de testar 1G, 2G, 3G, ... (força bruta),
#  o BSGS divide k em duas partes usando o truque:
#
#      k = i·m + j        onde m = ⌈√n⌉  e  n = ordem do grupo
#
#  Logo:   Q = k·G  →  Q = (i·m + j)·G  →  Q - i·m·G = j·G
#
#  Baby Steps: calculamos j·G para j = 0..m-1  → guardamos numa tabela
#  Giant Steps: calculamos Q - i·(m·G) para i = 0..m  → procuramos na tabela
#
#  Quando a tabela bate (colisão): k = i·m + j  → chave encontrada!
#
#  Complexidade: O(√n) operações — muito melhor que O(n) da força bruta!
# ============================================================

import math

# --- Parâmetros da curva e do corpo finito ---
p = 97   # primo que define o corpo finito F_97
a = 3    # coeficiente 'a' da curva
b = 6    # coeficiente 'b' da curva
# Equação: y² ≡ x³ + 3x + 6 (mod 97)

G = (0, 43)   # ponto gerador público  (ordem = 24)


# ============================================================
#  ARITMÉTICA EM CURVAS ELÍPTICAS
# ============================================================

def inverso_modular(k, p):
    """Inverso modular de k em F_p  (equivale a 'dividir por k' no módulo p)."""
    return pow(k, -1, p)


def soma_pontos(P, Q):
    """Soma dois pontos P e Q na curva elíptica."""
    if P is None: return Q          # ponto no infinito é o elemento neutro
    if Q is None: return P

    x1, y1 = P
    x2, y2 = Q

    # P + (−P) = ponto no infinito
    if x1 == x2 and (y1 + y2) % p == 0:
        return None

    # Inclinação λ da reta
    if P == Q:                      # dobramento de ponto
        lamb = (3 * x1**2 + a) * inverso_modular(2 * y1, p)
    else:                           # soma de dois pontos distintos
        lamb = (y2 - y1) * inverso_modular(x2 - x1, p)

    lamb %= p
    x3 = (lamb**2 - x1 - x2) % p
    y3 = (lamb * (x1 - x3) - y1) % p
    return (x3, y3)


def multiplicacao_escalar(k, P):
    """
    Calcula k·P pelo método double-and-add.
    Muito mais rápido que somar P exatamente k vezes.
    """
    resultado = None   # ponto no infinito (elemento neutro)
    base = P
    while k > 0:
        if k % 2 == 1:
            resultado = soma_pontos(resultado, base)
        base = soma_pontos(base, base)
        k //= 2
    return resultado


def calcular_ordem(P):
    """Calcula a ordem do ponto P: menor n > 0 tal que n·P = ponto no infinito."""
    cur = P
    n = 1
    while cur is not None:
        cur = soma_pontos(cur, P)
        n += 1
    return n


# ============================================================
#  CONFIGURAÇÃO DO ATAQUE
# ============================================================

chave_privada_real = 17          # o atacante NÃO conhece esse valor
Q = multiplicacao_escalar(chave_privada_real, G)   # chave pública (conhecida pelo atacante)

n = calcular_ordem(G)            # ordem do grupo
m = math.isqrt(n) + 1           # m = ⌈√n⌉

print("=" * 60)
print("  Baby-Step Giant-Step – Ataque ao ECDLP")
print("=" * 60)
print(f"\n  Curva : y² ≡ x³ + {a}x + {b} (mod {p})")
print(f"  Gerador  G = {G}")
print(f"  Chave pública Q = {Q}  (= {chave_privada_real}·G, desconhecida)")
print(f"\n  Ordem do grupo  n = {n}")
print(f"  Tamanho do passo m = ⌈√{n}⌉ = {m}")
print(f"\n  Objetivo: encontrar k tal que k·G = Q\n")


# ============================================================
#  FASE 1 – BABY STEPS
#  Calcula j·G para j = 0, 1, ..., m-1
#  e armazena na tabela:  ponto → j
# ============================================================
print("-" * 60)
print("  FASE 1 – Baby Steps  (preencher tabela de referência)")
print("-" * 60)

tabela_baby = {}

ponto = None          # j=0: 0·G = ponto no infinito
for j in range(m):
    tabela_baby[ponto] = j
    label = str(ponto) if ponto else "∞ (ponto no infinito)"
    print(f"    j={j:2d} → {j}·G = {label}")
    ponto = soma_pontos(ponto, G)

print(f"\n  Tabela preenchida com {len(tabela_baby)} entradas.\n")


# ============================================================
#  FASE 2 – GIANT STEPS
#  Calcula Q − i·(m·G) para i = 0, 1, ...
#  Se o resultado estiver na tabela → colisão encontrada!
#
#  Q − i·m·G = j·G   ⟹   Q = (i·m + j)·G   ⟹   k = i·m + j
# ============================================================
print("-" * 60)
print("  FASE 2 – Giant Steps  (procurar colisão na tabela)")
print("-" * 60)

mG     = multiplicacao_escalar(m, G)       # m·G  (o "passo gigante")
neg_mG = (mG[0], (-mG[1]) % p)            # −(m·G) para subtrair a cada passo

chave_encontrada = None
gigante = Q      # começa em Q − 0·(m·G) = Q

for i in range(m + 1):
    label = str(gigante) if gigante else "∞"
    print(f"    i={i:2d} → Q − {i}·{m}·G = {label}", end="")

    if gigante in tabela_baby:
        j = tabela_baby[gigante]
        chave_encontrada = i * m + j
        print(f"  ← COLISÃO com j={j} da tabela!  k = {i}·{m} + {j} = {chave_encontrada}")
        break

    print()
    gigante = soma_pontos(gigante, neg_mG)   # subtrai m·G a cada iteração


# ============================================================
#  RESULTADO FINAL
# ============================================================
print("\n" + "=" * 60)
if chave_encontrada is not None:
    verificacao = multiplicacao_escalar(chave_encontrada, G)
    status = "✓ Correto!" if verificacao == Q else "✗ Erro!"
    print(f"  Chave privada encontrada:  k = {chave_encontrada}")
    print(f"  Verificação: {chave_encontrada}·G = {verificacao}")
    print(f"               Q             = {Q}")
    print(f"  {status}")
else:
    print("  Chave não encontrada.")
print("=" * 60)

```

---

# **3.4.3 Ataques de Canal Lateral**

Além de ataques puramente matemáticos, implementações de ECC podem sofrer ataques de canal lateral (_side-channel attacks_).

Esses ataques exploram informações físicas do dispositivo durante a execução do algoritmo.

Exemplos:

- tempo de execução
    
- consumo de energia
    
- emissão eletromagnética
    
- uso de cache
    

Mesmo que o algoritmo matemático seja seguro, falhas de implementação podem comprometer completamente o sistema.

---

# **3.4.4 Computação Quântica**

Assim como ocorre com o RSA, algoritmos quânticos representam uma ameaça futura ao ECC.

O algoritmo de Shor é capaz de resolver o Problema do Logaritmo Discreto em tempo polinomial utilizando computadores quânticos suficientemente avançados.

Por esse motivo, atualmente existe um grande esforço internacional no desenvolvimento da chamada:

$$  
\text{Criptografia Pós-Quântica}  
$$

---

# **3.5 Pontos Fortes e Limitações do ECC**

## **Vantagens**

- chaves menores
    
- alta eficiência
    
- menor consumo energético
    
- excelente segurança criptográfica
    
- ideal para dispositivos móveis e sistemas embarcados
    

## **Limitações**

- matemática mais complexa
    
- implementação mais difícil
    
- vulnerabilidade a ataques quânticos
    
- necessidade de curvas cuidadosamente escolhidas
    

---

# **4. Conclusão**

A Criptografia de Curvas Elípticas representa uma das tecnologias mais importantes da criptografia moderna.

Seu principal diferencial está na capacidade de oferecer alto nível de segurança utilizando chaves significativamente menores que as utilizadas pelo RSA.

Ao longo deste trabalho, foram apresentados os fundamentos matemáticos básicos do ECC, incluindo aritmética modular, curvas elípticas, soma de pontos e multiplicação escalar.

Também foram discutidas aplicações práticas como ECDH e ECDSA, amplamente utilizados em protocolos modernos de segurança digital.

A análise dos algoritmos de ataque demonstrou que a segurança do ECC depende diretamente da dificuldade do Problema do Logaritmo Discreto em Curvas Elípticas.

Mesmo ataques mais sofisticados, como Baby-Step Giant-Step, tornam-se inviáveis para curvas modernas corretamente implementadas.

Os exemplos desenvolvidos em Python permitiram visualizar de forma prática como operações envolvendo curvas elípticas funcionam computacionalmente.

Isso contribui significativamente para o entendimento da aplicação da matemática na segurança da informação e no desenvolvimento de sistemas computacionais seguros.

Por fim, conclui-se que o ECC continuará desempenhando papel fundamental na criptografia moderna, especialmente em aplicações que exigem eficiência, baixo consumo de recursos e alta segurança.

---

# **5. Referências**

STALLINGS, William. Cryptography and Network Security: Principles and Practice. 7. ed. Pearson, 2017.

HANKERSON, Darrel; MENEZES, Alfred; VANSTONE, Scott. Guide to Elliptic Curve Cryptography. Springer, 2004.

KATZ, Jonathan; LINDELL, Yehuda. Introduction to Modern Cryptography. CRC Press, 2014.

NIST. Recommended Elliptic Curves for Federal Government Use. Disponível em:

[https://csrc.nist.gov](https://csrc.nist.gov)

Acesso em: 2026.

SONG, Jimmy. Programming Bitcoin: Learn How to Program Bitcoin from Scratch. O'Reilly Media, 2019.

PYTHON SOFTWARE FOUNDATION. Python Documentation. Disponível em:

[https://docs.python.org](https://docs.python.org)

Acesso em: 2026.