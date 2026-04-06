### Nome: Gabriel Augusto de Lima Maia

**1a)**![[Desenho Exercício 1a|1000]]

**b)** Em um caso, a menina está tocando o pato com uma pena, já no outro caso ela está tocando em um pato que tem a posse de uma pena

**2a)** 

``` prolog
frase        --> expr_nominal, predicado.
expr_nominal --> artigo, nome.
expr_nominal --> artigo, nome, expr_propos.
predicado    --> verbo.
predicado    --> verbo, expr_nominal.
predicado    --> verbo, expr_nominal, expr_propos.
expr_propos  --> preposicao, expr_nominal.
nome         --> [menino]; [menina]; [pato]; [telescopio];                  [musica]; [pena].
preposicao   --> [com]; [ate].
verbo        --> [viu]; [esta]; [e]; [canta];                               [surpreende];[toca].
artigo       --> [um]; [uma]; [o]; [a].
```
**b)**

usando um comando como:

``` shell
?- Tokens = [a,menina,toca,o,pato,com,a,pena],
   findall(1, phrase(frase, Tokens), L),
   length(L, N).
```
e

```shell
?- Tokens = [a,menina,toca,o,pato],
   findall(1, phrase(frase, Tokens), L),
   length(L, N).
```

o resultado vai dar 2 e 1 respectivamente.

**c)**

São seis possíveis soluções pois sujeito é um nome e pode ser qualquer um dos 6 tipos de nomes na gramática.

**3)**

```c
a = ((b < c) ? ((* p) + (b * c)) : (1 << (d ())))
```

**4a)**
![[Desenho 2 Exercício 1]]

**b)**

Como podemos ver na arvore, por causa da ambiguidade, a gramatica permite a soma da direita para a esquerda e da esquerda para a direta, sendo que matematicamente, o correto é da esquerda para a direita.

**c)**

```
<exp>    ::= <exp> + <sumexp>
			 | <sumexp>
<sumexp> ::= <number>
```

**5)**
 A primeira tem ambiguidade como podemos ver nessa arvore:
 
 ![[Exemplo 3 Exercicio 1|1000]]
 Já a segunda não tem esse problema porque toda string não vazia começa obrigatoriamente com uma parenteses ou um colchete forçando uma unica decomposição.
 
 **6a)** Significa que ele agrupa as operações da esquerda para a direita e resolve da esquerda para a direita.
 
 **b)**  ele é associativo à esquerda.
 
 **c)** o =,+=,-=, são exemplos de associativos a direita.

**d)** 
```
<exp> ::= <exp> + <mulexp> 
			| <mulexp>
<mulexp> ::= <mulexp> * <rootexp> 
			| <rootexp>
<rootexp> ::= ( <exp> )
			| <number>
```
 
 **7a)**
``` prolog
exp(N) --> exp(N1), [+], mulexp(N2), {N is N1 + N2}.

exp(N) --> mulexp(N).

mulexp(N) --> mulexp(N1), [*], rootexp(N2), {N is N1 * N2}.

mulexp(N) --> rootexp(N).

rootexp(N) --> ['('], exp(N),[')'].

rootexp(N) --> num(N).

num(X,[X|L],L) :- number(X).
 
```
**b)**
```prolog
expr(N) --> mulexp(N2) , [+],expr(N1) , {N is N1 + N2}.

expr(N) --> mulexp(N).

mulexp(N) --> rootexp(N2) , [*],mulexp(N1) , {N is N1 * N2}.

mulexp(N) --> rootexp(N).

rootexp(N) --> ['('], expr(N),[')'].

rootexp(N) --> num(N).

num(X,[X|L],L) :- number(X).
```

