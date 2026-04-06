**1a)**
```sml
fun power b e = let
    fun aux b e acc = 
        if e = 0 then acc
        else aux b (e-1) (acc * b)
in
    aux b e 1
end;

```

**b)**

```
fun binary n =
  let
    fun aux (0, acc) = acc
      | aux (m, acc) = aux (m div 2, (m mod 2) :: acc)
  in
    if n = 0 then [0]
    else aux (n, [])
  end;

```

**2a)**

```prolog
fact(N, R) :-
    fact_acc(N, 1, R).

fact_acc(0, Acc, Acc).
fact_acc(N, Acc, R) :-
    N > 0,
    Acc1 is Acc * N,
    N1 is N - 1,
    fact_acc(N1, Acc1, R).

```

**b)**


```prolog
addup(L, R) :-
    addup_acc(L, 0, R).

addup_acc([], Acc, Acc).
addup_acc([X|L], Acc, R) :-
    Acc1 is Acc + X,
    addup_acc(L, Acc1, R).


```
**3a)**

predicado para verificar se tem uma lista vazia entre duas listas.
```prolog
riddle([], _).
riddle(_, []).

```

**b)** predicado para verificar qual o ultimo elemento

```prolog
mystery(Item, [Item]).
mystery(Item, [_|T]) :-
    mystery(Item, T).

```

**c)** percorre a lista e inclui E em todos os elementos

```prolog
puzzle(_, [], []).
puzzle(E, [_|Tail], [E|ResultTail]) :-
    puzzle(E, Tail, ResultTail).

```

**4)**

```prolog
rev_filter([], _, []).
rev_filter([Head|Tail], E, Result) :-
    ( Head == E ->
        rev_filter(Tail, E, Result)
    ;
        rev_filter(Tail, E, TailResult),
        Result = [Head|TailResult]
    ).


```
**5)**

```
fun prefixCopy x n =
  let
    fun revAppend (nil, ys) = ys
      | revAppend (h::t, ys) = revAppend (t, h::ys)
    fun aux (xs, k, acc) =
      if k = 0 then
        revAppend (acc, xs)
      else
        case xs of
            nil => revAppend (acc, nil)  
          | h::t => aux (t, k-1, h::acc) 
  in
    if n <= 0 then x
    else aux (x, n, nil)
  end

```

Para listas grandes (ou `n` grande), a versão em cauda é geralmente “mais eficiente” no sentido importante do modelo de custo: **evita crescer a pilha** e reduz risco de stack overflow.

**6)**
