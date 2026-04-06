**1)**

A ideia de **Encapsulamento** é esconder detalhes internos e expor apenas o que é necessário na interface, isso protege variáveis que não queremos que sejam mudadas e evita o uso incorreto delas. Em Lua, a forma mais forte é via **clausuras** (closures), não via “privado” de classe.

```lua
-- Conta bancária com saldo "privado" (só acessível pelas funções retornadas)
function novaConta(dono, inicial)
  local saldo = inicial or 0  -- privado na clausura
  return {
    dono = dono,
    depositar = function(_, v)
      assert(v > 0, "depósito deve ser positivo")
      saldo = saldo + v
    end,
    sacar = function(_, v)
      assert(v <= saldo, "saldo insuficiente")
      saldo = saldo - v
    end,
    saldo = function(_) return saldo end
  }
end

-- uso
local c = novaConta("Ana", 100)
c:depositar(50)
print(c:saldo())   -- 150
-- print(c.saldoVar)  --> inexistente; não há como “vazar” o saldo interno


```

Já a ideia de **Herança** é a de criar classes especializadas que reaproveitam comportamentos de uma classe base.

```lua
-- Classe base: Forma
Forma = {}
Forma.__index = Forma

function Forma:new()
  return setmetatable({}, self)
end

function Forma:area()
  error("Forma: área não definida")
end

-- Subclasse: Retangulo
Retangulo = setmetatable({}, { __index = Forma })
Retangulo.__index = Retangulo

function Retangulo:new(l, a)
  local obj = Forma.new(self)
  obj.l = l
  obj.a = a
  return obj
end

function Retangulo:area()
  return self.l * self.a
end

-- Subclasse: Circulo
Circulo = setmetatable({}, { __index = Forma })
Circulo.__index = Circulo

function Circulo:new(r)
  local obj = Forma.new(self)
  obj.r = r
  return obj
end

function Circulo:area()
  return math.pi * self.r * self.r
end

-- uso
local r = Retangulo:new(3, 4)
local c = Circulo:new(2)
print(r:area())  -- 12
print(c:area())  -- 12.566...

```

A ideia de **Composição** é a de montar objetos maiores a partir de objetos menores("tem,um"), em vez de herdar("é-um").

```lua
-- Componentes
Motor = {}; Motor.__index = Motor
function Motor:new(hp) return setmetatable({hp = hp, ligado = false}, self) end
function Motor:ligar() self.ligado = true end
function Motor:desligar() self.ligado = false end

Tanque = {}; Tanque.__index = Tanque
function Tanque:new(capL) return setmetatable({cap = capL, nivel = capL}, self) end
function Tanque:consumir(l)
  assert(l <= self.nivel, "Sem combustível")
  self.nivel = self.nivel - l
end

-- Agregador
Carro = {}; Carro.__index = Carro
function Carro:new(motor, tanque)
  return setmetatable({motor = motor, tanque = tanque}, self)
end

function Carro:dirigir(km)
  if not self.motor.ligado then self.motor:ligar() end
  local consumo = km / 12.0   -- 12 km/L (exemplo)
  self.tanque:consumir(consumo)
  return string.format("Andou %.0f km; restam %.1f L", km, self.tanque.nivel)
end

-- uso
local carro = Carro:new(Motor:new(100), Tanque:new(40))
print(carro:dirigir(24))  -- consome 2 L

```

A ideia de **Polimorfismo** é usar objetos diferentes de forma uniforme pelo mesmo método/interface.

Usando duck typing (sem herança):

```lua
local CSV = {}
function CSV:exportar(tabela)
  local linhas = {}
  for _, linha in ipairs(tabela) do
    local cols = {}
    for _, v in ipairs(linha) do table.insert(cols, tostring(v)) end
    table.insert(linhas, table.concat(cols, ","))
  end
  return table.concat(linhas, "\n")
end

local JSON = {}
function JSON:exportar(tabela)
  -- JSON bem simples (só pra exemplo)
  local linhas = {}
  for _, linha in ipairs(tabela) do
    local cols = {}
    for _, v in ipairs(linha) do table.insert(cols, tostring(v)) end
    table.insert(linhas, "[" .. table.concat(cols, ",") .. "]")
  end
  return "[" .. table.concat(linhas, ",") .. "]"
end

local function salvarRelatorio(dados, exportador)
  -- qualquer objeto que tenha :exportar(dados) serve
  local blob = exportador:exportar(dados)
  print(blob)
end

salvarRelatorio({{1,2},{3,4}}, CSV)
salvarRelatorio({{1,2},{3,4}}, JSON)


```

usando por herança, reaproveitando forma/retângulo/circulo do exemplo acima:

```lua
local formas = { Retangulo:new(2,5), Circulo:new(1.5) }

local function somaAreas(fs)
  local total = 0
  for _, f in ipairs(fs) do
    total = total + f:area()  -- chamada polimórfica
  end
  return total
end

print(somaAreas(formas))


```

**2)** A saida vai ser:

```makefile
Nome: Joao
CPF: 12345678901
```

A chamada polimórfica ocorre **em tempo de execução**, quando o Java identifica que o objeto armazenado em `p` é do tipo `PessoaFisica`, e portanto executa a versão sobrescrita de `print()` dessa classe.

**3a)**

```cpp
#include <iostream>
#include <string>
#include <memory>

class Pessoa {
private:
    std::string nome;

public:
    explicit Pessoa(std::string nome) : nome(std::move(nome)) {}
    virtual ~Pessoa() = default;                 // importante para deletar via ponteiro base

    // virtual garante ligação tardia (late binding)
    virtual void print() const {
        std::cout << "Nome: " << nome << '\n';
    }
};

class PessoaFisica : public Pessoa {
private:
    long long cpf;

public:
    PessoaFisica(std::string nome, long long cpf)
        : Pessoa(std::move(nome)), cpf(cpf) {}

    // override: sobrescreve o método virtual da base
    void print() const override {
        Pessoa::print();                         // equivalente ao super.print() do Java
        std::cout << "CPF: " << cpf << '\n';
    }
};

int main() {
    // Tipo estático: Pessoa; tipo dinâmico (real): PessoaFisica
    std::unique_ptr<Pessoa> p = std::make_unique<PessoaFisica>("Joao", 12345678901LL);
    p->print();   // chamada polimórfica: escolhe PessoaFisica::print() em tempo de execução
    return 0;
}

```

**b)**

Existem duas formas, uma retirando o virtual da superclasse, assim ele vai chamar sempre a versão da superclasse. ou podemos fazer uma chamada explícita usando `obj.Base::método()` que força a execução da base, mesmo com o virtual declarado.

**4)**

```cpp
#include <iostream>

class S {
private:
    // 1. Construtor privado → ninguém fora da classe pode criar S diretamente
    S() {
        std::cout << "Instância criada!\n";
    }

    // 2. Instância estática única (lazy initialization)
    static S* instancia;

public:
    // 3. Método público e estático que retorna a instância
    static S* instance() {
        if (instancia == nullptr) {
            instancia = new S(); // cria só na primeira chamada
        }
        return instancia;
    }

    // 4. Impedir cópia ou atribuição (mantém unicidade)
    S(const S&) = delete;
    S& operator=(const S&) = delete;

    // Exemplo de método normal da classe
    void sayHello() const {
        std::cout << "Olá! Sou o Singleton S.\n";
    }
};

// 5. Definição do ponteiro estático fora da classe
S* S::instancia = nullptr;

int main() {
    // Todas as variáveis apontam para a MESMA instância
    S* a = S::instance();
    S* b = S::instance();

    a->sayHello();
    b->sayHello();

    // Mostra que são o mesmo objeto
    std::cout << "Endereço de a: " << a << "\n";
    std::cout << "Endereço de b: " << b << "\n";
}

```

**5**

Em java, os **Generics** permitem declarar classes e métodos parametrizados por tipo.

Internamente, durante a compilação, o java verifica os tipos, que são genéricos. Mas na execução, o tipo genérico é apagado, ou seja, o bytecode usa apenas objetos.

isso ajuda com a segurança de tipos em tempo de compilação e evita erros de tipo e tem retrocompatibilidade. 

Já em C++, os **templates** são instruções para o compilador gerar código especializado para cada tipo usado.

Assim, o compilador gera uma cópia do código da classe/função para cada tipo usado. isso ajuda a não ter apagamento de tipo (type erasure) e funciona com qualquer tipo. porém pode gerar código duplicado.

resumindo:

**Java Generics** = segurança de tipo em tempo de compilação, mas sem manter o tipo real (apagamento).  
**C++ Templates** = geram código especializado em tempo de compilação, com desempenho e flexibilidade maiores, mas custo de binário e mensagens de erro maiores.

**6)**

 Não tem erro de execução, imprime:
 
 0
E::p
1
1
1

**7)**