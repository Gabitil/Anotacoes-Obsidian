

_Linguagens de Programação – Engenharia da Computação_
**Aluno:** Gabriel Augusto de Lima Maia
**Instituição:** CEFET-MG

Data de Entrega: 24/11/2025

# Introdução

Este documento apresenta seis funcionalidades modernas, idiomáticas e relevantes da linguagem PHP, destacando aspectos de sua sintaxe e semântica que a diferenciam de linguagens como C, C++ e Java. Para cada funcionalidade, são exibidos exemplos de código, explicações detalhadas de funcionamento e justificativas que evidenciam sua utilidade prática e seu impacto no estilo de programação adotado em PHP.
  
  

## Funcionalidade 1 – Match  


#### Código:

```php
$nota = 8;
 
$conceito = match (true) {
	$nota >= 9 => "A",
	$nota >= 7 => "B",
	$nota >= 5 => "C",
	default => "D",
};

echo $conceito;
```


#### Explicação:

A expressão avalia condições booleanas com a técnica `match(true)` e retorna o primeiro braço cujo teste é `true`. Com `$nota = 8` o resultado será `"B"` (porque `8 >= 9` é falso, `8 >= 7` é verdadeiro).

**Passo a passo**

1. `$nota = 8;` inicializa a variável usada nos testes, permitindo demonstrar o comportamento condicional do `match`.
2. match (true) { ... } — cada entrada testa uma expressão booleana:
    - `$nota >= 9 => "A"`: se for verdade retorna "A".
    - `$nota >= 7 => "B"`: se for verdade retorna "B".
    - `$nota >= 5 => "C"`: se for verdade retorna "C".
    - `default => "D"`: caso nenhum anterior seja verdade retorna "D".
3. O valor retornado por match é atribuído a $conceito.
4. echo $conceito; — imprime o conceito (no caso: B).
   


#### Justificativa:

O match em PHP transforma um conjunto de verificações em uma expressão que retorna um valor de forma concisa, segura e sem fall‑through (que é o que acontece quando você esquece de por o break no fim da instrução do case e ele continua para o próximo case, causando alguns bugs comuns em outras linguagens).

**Pontos importantes**

**1-** `match` usa comparação estrita: `match ($x) { 0 => 'zero' }` não casará se `$x === '0'` (string). Por outro lado, `switch` com `==` poderia casar.

**2-**  `match` não permite duplicidade de chaves; chaves duplicadas resultam em erro.

**3-**  Sem `default`, `match` lança `UnhandledMatchError` ou seja, temos que tratar ou fornecer `default`.

**4-** Ordem importa: o match pega o primeiro braço do teste que o  resultado é `true`.

## Funcionalidade 2 - Union types
#### **Código:**

```php
function formatarId(int|string $id): string {
	return "ID: $id";
} 

echo formatarId(10);
echo formatarId("abc");
```

#### Explicação:

A função aceita valores de dois tipos distintos (`int` ou `string`). Union types permitem declarar explicitamente que um parâmetro pode assumir múltiplos tipos válidos. Caso seja passado um tipo incompatível, o PHP lança um `TypeError`.

#### Justificativa:

Union types aprimoram a expressividade e a documentação automática do código, permitindo funções mais flexíveis e autodescritivas sem sacrificar segurança. Em C/C++ e Java, esse comportamento requer abstrações mais complexas (como `std::variant`, `Object` ou sobrecarga de métodos). No PHP, a sintaxe é nativa e minimalista, tornando o recurso extremamente útil em APIs modernas.
## Funcionalidade 3 - Nullsafe operator `?->` + Null coalescing `??`

#### Código:

```php
class Perfil { public ?string $bio; }

$perfil = null;

echo $perfil?->bio ?? "Sem bio";
```

#### Explicação:

**Passo a passo:**

- Declara a classe Perfil com a propriedade typed que pode ser string ou null:
	- class Perfil { public ?string $bio; }
- Define $perfil = null;
- Faz um echo com duas operações:
	- ?-> (nullsafe operator): tenta acessar bio somente se $perfil não for null; se $perfil for null, a expressão inteira retorna null em vez de lançar erro.
	- ?? (null coalescing): se o lado esquerdo for null, usa o valor à direita ("Sem bio").

#### Justificativa:

Substitui checagens verbosas (`if ($perfil !== null && $perfil->bio !== null)`) por uma expressão curta e legível. Em linguagens como C, C++ e Java isso exigiria muitos testes manuais ou classes opcionais. PHP resolve com sintaxe compacta e segura, melhorando legibilidade e reduzindo erros comuns, como  o erro fatal “trying to access property on null” sem precisar escrever código de verificação manual. 

Melhora bastante a legibilidade também, mostra claramente “pegue bio se existir, senão use um padrão”, o que melhora a documentação implícita do código.

## Funcionalidade 4 -  Argumentos Nomeados

#### Código:

```php
function criarUsuario($nome, $idade, $admin = false) {

echo "$nome ($idade) admin? $admin";

}

criarUsuario(idade: 20, nome: "Ana", admin: true);
```

#### Explicação:

**Passo a passo:**

**1-** Definimos a função criarUsuario.
	- Parâmetros: $nome, $idade e $admin (opcional, padrão false).
	- o echo imprime uma string interpolada com as variáveis.
**2-** Chamada da função com named arguments.
```php
	criarUsuario(idade: 20, nome: "Ana", admin: true);
```
-  Usa argumentos nomeados (named arguments), portanto a ordem na chamada não importa desde que os nomes existam.
  
  **Comportamento/saida esperada:**

- Em PHP 8+, a chamada é válida. A saída será:  
    Ana (20) admin? 1
#### Justificativa:

A chamada usa nomes dos parâmetros em vez de posição, isso melhora legibilidade quando uma função tem muitos parâmetros ou parâmetros opcionais. Você não precisa memorizar a ordem. Além disso,  o uso de `nome:` e `idade:` torna o chamado autoexplicativo, o que facilita a leitura do código por terceiros.

**Outras linguagens**

- PHP tem named arguments nativos (introduzidos no PHP 8). Linguagens como:
    - **Python**: tem kwargs / named args similares.
    - **JavaScript/TypeScript**: não têm named args nativos — costuma-se passar um objeto com propriedades para simular.
    - **Java**: não tem named args; precisa de builders ou objetos de parâmetro.
    - **C# / Kotlin**: têm named arguments nativos (semelhante ao PHP).
      
- Diferença importante em PHP: os argumentos são ligados pelo **nome do parâmetro** no momento da chamada — renomear o parâmetro na definição da função pode quebrar chamadas que usarem named args. Isso é diferente de passar um objeto (JS) que não depende de nomes de parâmetros da função.
## Funcionalidade 5 - Generators e `yield`

#### Código:

```php
function gen_one_to_three() {
	for ($i = 1; $i <= 3; $i++) {
		// Observe que $i é preservado entre chamadas.
		yield $i;
	}
}
$generator = gen_one_to_three();
foreach ($generator as $value) {
	echo "$value\n";
}
```

#### Explicação:

**Passo a passo:**

**1-  Vamos observar a função `gen_one_to_three`:**
- Essa função **não retorna um array completo de uma vez**.
- Em vez disso, ela é um **generator**: cada vez que o código externo pedir o próximo valor, ela executa até encontrar um `yield`.
- O `yield $i;`:
    - “entrega” o valor atual de `$i` para quem está iterando.
    - **pausa** a execução da função naquele ponto.
    - na próxima iteração, a função **continua exatamente de onde parou**, com o valor de `$i` preservado.

Em termos de comportamento, essa função gera a sequência 1,2,3 sob demanda, um valor por vez.

**2-  Criando o generator `$generator = gen_one_to_three();`**
	Aqui nós não estamos recebendo um array `[1, 2, 3]`. Estamos recebendo um **objeto Generator**, que sabe como produzir esses valores quando for iterado.
  
**3- Iterando sobre o generator `foreach ($generator as $value) {echo "$value\n";}`**

O `foreach` faz o seguinte:

1. Pede o primeiro valor ao generator:
    - A função `gen_one_to_three()` roda o `for` até o primeiro `yield`. `yield` devolve `1`.
2. O `foreach` coloca esse valor em `$value` e executa o bloco:
    - `echo "1\n";`
3. Pede o próximo valor:
    - A função continua do ponto após o primeiro `yield`, incrementa `$i` para `2`, encontra o próximo `yield`.
    - `yield` devolve `2`.
    - Imprime `2\n`.
4. Repete para `3`.
5. Quando `$i` passa de `3`, o `for` termina, o generator não tem mais valores, e o `foreach` para.

**4- Saída do programa**

O comportamento visível é:

```
1
2
3
```

Cada número em uma linha.
#### Justificativa:

Generators permitem iterar sobre sequências grandes sem armazenar todos os elementos na memória, reduzindo uso de recursos. 

Embora linguagens modernas possuam mecanismos similares (como Python e C#), linguagens como C e Java tradicional requerem estruturas mais verbosas. No PHP, esse recurso é nativo, simples e poderoso, e ainda oferece funcionalidades avançadas como `yield from`, `send()` e controle preciso sobre o fluxo.

## Funcionalidade 6 - Anonymous class

#### Código:

```php
$logger = new class {
	public function log($msg) {
		echo "[LOG] $msg\n";
	}
}; 

$logger->log("teste");
```

#### Explicação:

- `new class { ... }` cria uma **classe anônima** e já instancia um objeto dessa classe.
- Esse objeto é guardado em `$logger`.
- O método `log` imprime a mensagem prefixada com `[LOG]`.
- `\$logger->log("teste");` produz na saída `[LOG] teste`.

#### Justificativa:

Classes anônimas permitem criar objetos utilitários sem ocupar o namespace com nomes adicionais, sendo ideais para pequenos comportamentos locais, testes e padrões de projeto leves. Embora existam classes internas anônimas em Java, a sintaxe é significativamente mais verbosa; em C e C++ o recurso praticamente não existe. No PHP, esse mecanismo é simples, direto e integrado ao modelo orientado a objetos.


#  **Referências**

### Documentação Oficial do PHP

- Match Expression: [https://www.php.net/manual/pt_BR/control-structures.match.php](https://www.php.net/manual/pt_BR/control-structures.match.php)
- Sistema de Tipos e Union Types: [https://www.php.net/manual/pt_BR/language.types.type-system.php](https://www.php.net/manual/pt_BR/language.types.type-system.php)
- Nullsafe Operator (PHP 8): [https://www.php.net/releases/8.0/en.php](https://www.php.net/releases/8.0/en.php)
- Null Coalescing Operator: [https://www.php.net/manual/en/migration70.new-features.php](https://www.php.net/manual/en/migration70.new-features.php)
- Argumentos Nomeados: [https://www.php.net/manual/pt_BR/functions.arguments.php](https://www.php.net/manual/pt_BR/functions.arguments.php)
- Generators: [https://www.php.net/manual/pt_BR/language.generators.syntax.php](https://www.php.net/manual/pt_BR/language.generators.syntax.php)
- Anonymous Classes: [https://www.php.net/manual/pt_BR/language.oop5.anonymous.php](https://www.php.net/manual/pt_BR/language.oop5.anonymous.php)