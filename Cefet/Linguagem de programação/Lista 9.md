**1a)** tem os parâmetros da função, variáveis locais, endereço de retorno, link dinâmico, link de aninhamento.

**b)**
Porque C não tem funções aninhadas com acesso a variáveis não locais do escopo externo. Assim, não há necessidade de “subir” pela cadeia léxica em tempo de execução: ou a variável é local (está no RA atual) ou é global/estática (tem endereço conhecido/estático). Logo, basta o link dinâmico para voltar ao chamador; link de aninhamento seria inútil.

**2)**

**3)** Na chamada da função interna, o RA recebe um link de aninhamento (SL) apontando para o RA da função imediatamente externa. Para acessar a variável que mora “m níveis acima”, o runtime segue o `SL` exatamente `m` vezes (saltos) até o RA correto. Dentro desse RA alvo, a variável é acessada pelo deslocamento (offset) conhecido em compilação.

O Por que de não precisar de um caso especial  para quando `m > n` é porque esse caso não acontece, uma função não pode referenciar variáveis de escopos mais internos do que ela . Se alguém escreveu algo que exigiria `m > n`, não é uma referência legítima — o compilador rejeita. Portanto, não há caso operacional `m > n`.

**4a)**
```sml
fun fact 0 = 1
  | fact n = n * fact (n - 1)

```
**b)**

```sml
fun outer x =
  let
    fun inner y = x + y   
  in
    inner 1
  end

```
**5a)**
Pode desalocar. Retorna apenas um `int`; não há closure escapando.

**b)**

Não pode desalocar. Retorna uma função que captura x; o ambiente (ou ao menos x) precisa sobreviver

**c)**

Pode desalocar. A função retornada não captura x. O RA de f não é necessário após o retorno.

**d)**

Não pode desalocar. `map x` é aplicação parcial; retorna uma função que captura `x` (o comparador/transformador passado), portanto o ambiente precisa sobreviver.

**6a)**
Não. A `f` não referencia variáveis externas (apenas seu parâmetro `x`). Sua closure é vazia; ao ser chamada por `map`, não precisa seguir link de aninhamento.

**b)**
Usa, `f` captura `n` do escopo externo; quando `map` chama `f`, ela precisa acessar `n` via o link de aninhamento

**c)**
não há uso do link de aninhamento para o RA de `do123`, Quando `map` chama `f`, ele usará o link/ambiente que já veio com `f`