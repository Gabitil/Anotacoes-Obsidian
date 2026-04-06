**1)a)** não unifica
**b)** unifica, resultado $X=2$ 
**c)** não unifica
**d)**  unifica, resultado da X= 3, Y= 3,  p(3,3)
**e)** não unifica
**f)** unifica, resultado = [7,3,4]
**g)** unifica e x= [];

**2a)** ![[Arvore 1]]
Aqui da backtracking já que não acha gosta(maria,peixe),gosta(pedro,peixe)

**b)**![[Arvore 2]]

**3a)** 

```prolog
nelementos([], 0).
nelementos([_|T], N) :-
    nelementos(T, N1),
    N is N1 + 1.
```
**b)**
```prolog
maior([X], X).

maior([H|T], H) :-
    maior(T, MT),
    H >= MT.

maior([H|T], MT) :-
    maior(T, MT),
    H < MT.


```

**c)**

```prolog
nelementos([], 0).
nelementos([_|T], N) :-
    nelementos(T, N1),
    N is N1 + 1.

soma([], 0).
soma([H|T], S) :-
    soma(T, S1),
    S is S1 + H.

medio(L, M) :-
    soma(L, S),
    nelementos(L, N),
    M is S / N.

```
**d)**

```
inserirfim(X, [], [X]).

inserirfim(X, [H|T], [H|R]) :-
    inserirfim(X, T, R).

```

**e)**
```
ultimo([X], X).

ultimo([_|T], U) :-
    ultimo(T, U).

```

**f)**

```
adjacente(X, Y, [X, Y | _]).

adjacente(X, Y, [_ | T]) :-
    adjacente(X, Y, T).

```

**g)**

```
gerar(N, N, [N]).

gerar(I, F, [I|R]) :-
    I < F,
    I1 is I + 1,
    gerar(I1, F, R).

```

**h)**
```
concatenar([], L, L).
concatenar([H|T], L, [H|R]) :-
    concatenar(T, L, R).

reverter([], []).

reverter([H|T], R) :-
    reverter(T, RT),
    concatenar(RT, [H], R).

```

**i)**
```
incrementar([], []).

incrementar([H|T], [H1|R]) :-
    H1 is H + 1,
    incrementar(T, R).

```
**j)**

```
concatenar([], L, L).
concatenar([H|T], L, [H|R]) :-
    concatenar(T, L, R).

linearizar([], []).

linearizar([H|T], L) :-
    linearizar(T, LT),
    concatenar(H, LT, L).

```

**k)**
```prolog
compactar([], []).

compactar([H|T], [[N,H] | R]) :-
    contar_consecutivos(H, T, N, Rest),
    compactar(Rest, R).

contar_consecutivos(H, [H|T], N, Rest) :-
    contar_consecutivos(H, T, N1, Rest),
    N is N1 + 1.

contar_consecutivos(H, [X|T], 1, [X|T]) :-
    H \= X.

contar_consecutivos(_, [], 1, []).

```
**l)**
```
remover(_, [], []).

remover(X, [X|T], R) :-
    remover(X, T, R).

remover(X, [H|T], [H|R]) :-
    X \= H,
    remover(X, T, R).

```

**m)**

```

inserirfim(X, [], [X]).
inserirfim(X, [H|T], [H|R]) :-
    inserirfim(X, T, R).

rotacionar([], []).
rotacionar([X], [X]).

rotacionar([H|T], R) :-
    inserirfim(H, T, R).

```

**n)**
```

inserirfim(X, [], [X]).
inserirfim(X, [H|T], [H|R]) :-
    inserirfim(X, T, R).


rotacionar([], []).
rotacionar([X], [X]).
rotacionar([H|T], R) :-
    inserirfim(H, T, R).


rotacionarn(0, L, L).

rotacionarn(N, L, R) :-
    N > 0,
    rotacionar(L, L1),
    N1 is N - 1,
    rotacionarn(N1, L1, R).

```

**o)**
```

ordenar([], []).


ordenar([H|T], L) :-
    ordenar(T, LT),            
    inserir_ordenado(H, LT, L). 

inserir_ordenado(X, [], [X]).


inserir_ordenado(X, [H|T], [X,H|T]) :-
    X =< H.


inserir_ordenado(X, [H|T], [H|R]) :-
    X > H,
    inserir_ordenado(X, T, R).

```