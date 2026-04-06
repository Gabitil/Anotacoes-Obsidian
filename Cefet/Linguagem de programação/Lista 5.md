### Nome: Gabriel Augusto de Lima Maia

**1)** 

Polimorfismo **ad-hoc** — **Sobrecarga**:

Um mesmo nome de função ou operador pode ter múltiplas implementações diferentes, escolhidas em tempo de compilação de acordo com o tipo dos argumentos. Exemplo em Java:

```java

public class Calculadora {

    public int soma(int a, int b) {
        return a + b;
    }


    public int soma(int a, int b, int c) {
        return a + b + c;
    }

    public double soma(double a, double b) {
        return a + b;
    }

    public static void main(String[] args) {
        Calculadora calc = new Calculadora();

        System.out.println(calc.soma(2, 3));
        System.out.println(calc.soma(1, 2, 3));
        System.out.println(calc.soma(2.5, 3.1));
    }
}
```

Polimorfismo **ad-hoc** — **Coerção:**

Um valor de um tipo é automaticamente convertido para outro tipo para que uma operação funcione. Exemplo em Lua:


```lua
print("10" + 5)  -- 15  (string "10" vira número)
print(10 .. 5)   -- "105" (número 10 vira string ao concatenar)

```


Polimorfismo **universal** — **Inclusão:**

Um objeto de um subtipo pode ser usado onde se espera o tipo base (herança ou interfaces). Exemplo em Lua:

```lua
Animal = {}
function Animal:new()
  local obj = {}
  setmetatable(obj, self)
  self.__index = self
  return obj
end
function Animal:falar() print("Som genérico") end

Cachorro = Animal:new()
function Cachorro:falar() print("Latido") end

a = Animal:new()
c = Cachorro:new()
a:falar() -- Som genérico
c:falar() -- Latido


```

Polimorfismo **universal** — **Paramétrico:**

Um código é escrito de forma genérica, funcionando para qualquer tipo passado como parâmetro. Exemplo em Python:

```python
from typing import TypeVar, Generic

T = TypeVar('T')

class Caixa(Generic[T]):
    def __init__(self, valor: T):
        self.valor = valor

def imprimir_caixa(c: Caixa[T]) -> None:
    print(c.valor)

c1 = Caixa(42)      # T = int
c2 = Caixa("texto") # T = str
imprimir_caixa(c1)
imprimir_caixa(c2)

```

**2a)** Aqui não é necessário, o tipos bytes são convertidos para int e guardados sem problema com $d = 20$.

**b)** Já aqui, em $b*2$ ,$b$ vira int já que 2 é int e o resultado da operação também vira int. Porém estamos tentando colocar um int dentro de um byte, e isso da erro de compilação.  para corrigir, fazemos:

```java
byte b = 50;
byte d = (byte) (b * 2);

```

e $d=100$



**3a)** **Precedência:** '`*`' tem maior precedência que '`+`' (pois `1 + 2 * 3 = 7`).

**Associatividade:** '`+`' é associativo à esquerda (pois `"1" + 2 + 3 = ("1"+2)+3 = "12"+3 = "123"`; se fosse à direita daria `"1"+(2+3) = "15"`).

```php
<Expr>   ::= <Expr> "+" <Term> | <Term>
<Term>   ::= <Term> "*" <Factor> | <Factor>
<Factor> ::= <INT> | <STRING> | "(" <Expr> ")"
```

**b)**

Só o '`+`'  precisa ser sobrecarregado

Para explicar `"1" + 2 + 3 -> "123"` e ao mesmo tempo `1 + "2*3"` ser erro, a linguagem precisa coagir `int -> string` apenas quando o operando esquerdo de `+` é `string`

Se `e1 : string` e `e2 : int`, então trata `e1 + e2` como  
`e1 + (int_to_string e2) : string`, onde  
`int_to_string : int -> string`.

e as operações de tipos dessa linguagem ficariam assim em ml:

```ml
(*) : int * int -> int
(+) : int * int -> int
(+) : string * string -> string
(+) : string * int -> string   (* usando coerção implícita int -> string *)

```
**c)** seria "16" (String)

**4 a)** É seguro
**b)** É seguro
**c)** Não seguro
**d)** Seguro
**e)** Não seguro
**f)** Não seguro
**g)** Seguro
**h)** Não seguro