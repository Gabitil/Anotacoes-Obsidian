
### Nome: Gabriel Augusto de Lima Maia

**1a)**

Temos definição de  classe na Linha 1, de método e  parâmetro na linha 2 e rótulo na linha 3.

**b)** Na Linha 1 temos a definição de Classe, depois temos:

- L2 (primeiro `Reuse`) – tipo de retorno  
    ⟶ definição da classe em L1 (`class Reuse`).
    
- L2 (terceiro `Reuse`) – tipo do parâmetro  
    ⟶ definição da classe em L1.
    
- L4 (primeiro `Reuse`) – qualificador antes do ponto (`Reuse.Reuse(...)`)  
    ⟶ definição da classe em L1.
    
- L4 (segundo `Reuse`) – nome do método chamado (`Reuse.Reuse(...)`)  
    ⟶definição do método em L2 (`Reuse Reuse(…)`).
    
- L4 (terceiro `Reuse`) – argumento da chamada  
    ⟶ definição do parâmetro em L2 (`(Reuse Reuse)`).
    
- L4 (quarto `Reuse`) – após `==`  
    ⟶ definição do parâmetro em L2.
    
- L5 (`break Reuse;`) – rótulo alvo do break  
    ⟶ definição do rótulo em L3 (`Reuse:`).  
    
- L7 (`return Reuse;`) – valor retornado  
    ⟶ definição do parâmetro em L2.
    


**2)** Observando esse comportamento, podemos dizer que a palavra-chave `var` possui escopo de função, ou seja, não é limitada pelos blocos como `if`, `for` ou `{}`.  

Assim, todas as declarações de `x` se referem à mesma variável dentro do mesmo escopo (no caso, o escopo global).  

Já com `let`, o escopo é de bloco, fazendo com que cada `x` seja uma variável diferente; por isso a saída passa a ser `3`, `2`, `1`, resolvendo de dentro para fora.

**3)** Em Bash, variáveis declaradas com `local` têm escopo restrito à função onde foram criadas. No exemplo, `x=3` é uma variável local de `f`, e por isso `g` acessa essa `x` durante a execução, sem alterar a variável global. Quando `f` termina, a variável local deixa de existir e o valor global de `x` permanece 1.

Se removermos `local`, a variável `x` passa a ter **escopo global**, sendo compartilhada entre todas as funções — nesse caso, o valor final impresso seria 2, resultando em 3 2 2.

**4a)**

No procedimento A, é visível a variável `u` e o subprograma `B`.

No procedimento B, é visível as variáveis `u(de A)`, `v(Local)` e os subprogramas visíveis são `C` e `F`

No procedimento C as variáveis visíveis são `u(de A)`, `v(de B)`, `x(Local)` e os subprogramas são `D` e `E`

No procedimento D as variáveis visíveis são, `u(Local)`, `x(de C)`, `v(de B)` e não tem subprogramas.

No procedimento E, as variáveis visíveis são, `v(Local)`, `u(de A)`, `x(de C)`

No procedimento F, as variáveis visíveis são, `y(Local)`, `v(de B)`, `u(de A)` e o subprograma visível é `G`

No procedimento G, as variaveis visíveis são, `x(Local)`, `y(de F)`, `v(de B)`, `u(de A)`

**b)** Uma solução seria mover a variável `u` para `A` ou `B`, assim, a variável `u` vira global dentro de B/G/D porém assim tanto G quanto D podem modificar a variável podendo ter complicações dependendo do que o programador quer fazer com o código.


