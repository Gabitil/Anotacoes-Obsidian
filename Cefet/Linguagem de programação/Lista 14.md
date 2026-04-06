**1)** Processos são mais pesados, eles tem controle sequencial e espaço separado de memoria, ou seja, cada processo é independente e a troca de contexto entre processos é mais custoso e depende de mecanismos do SO. Já threads é mais leves, eles sãos fluxos de execução dentro de um mesmo processo, porém eles não tem endereçamento proprio, compartilhando os recursos do processo pai, assim.

comunicação entre processos é feito explicitamente, já de threads pode ser tanto por cooperação quanto por competição.


**2)** **Paralelismo Real** envolve múltiplos processadores executando tarefas simultaneamente. Já **Paralelismo Aparente** envolve um único processador alternando entre tarefas rapidamente para dar a impressão de execução simultânea.

**3)** **Lockout (trancamento):** tarefa espera para sempre por uma condição que nunca ocorre.

**Exemplo:**

Duas threads precisam acessar um recurso e usam uma condição para prosseguir.  
Suponha que:

- A thread A precisa que `c > 0` para continuar.
    
- A thread B deveria aumentar `c`, mas nunca executa essa operação porque está esperando outra condição ou foi mal programada.

com isso A fica travado pra sempre.

**Deadlock (impasse):** tarefas ficam esperando mutuamente recursos → ninguém progride.

**Exemplo:**

- A thread A possui o `mutex1` e precisa do `mutex2`.
    
- A thread B possui o `mutex2` e precisa do `mutex1`.
  
Como ninguém consegue progredir, acontece o deadlock

**Starvation (inanição):** tarefa nunca recebe o recurso porque está sempre sendo preterida.

**Exemplo:**

Um semáforo é liberado frequentemente, mas sempre existe uma fila grande de threads de alta prioridade.  
Uma thread de baixa prioridade:

- Fica sempre atrás das outras na fila
    
- Nunca consegue acessar o recurso
    
- “Morre de fome”, sem nunca progredir

**Indeterminismo:** resultado imprevisível devido à ordem de execução concorrente.

### Exemplo:

Duas threads modificam a mesma variável global `g`:

- T1: `g *= 2`
    
- T2: `g += 3`
    

Dependendo de qual executa primeiro, os resultados podem ser:

- Se T1 depois T2 → `(10 * 2) + 3 = 23`
    
- Se T2 depois T1 → `(10 + 3) * 2 = 26`
    

O programa se torna **imprevisível**

**4)** **Semáforo binário** (0 ou 1) é usado para exclusão mútua — garante que apenas uma thread acesse a região crítica. **Semáforo genérico** (≥ 1) é usado quando há múltiplos recursos iguais — permite que várias threads acessem até o limite disponível.

Semáforo binário deve ser usado quando o recurso é único ou a região critica só pode ser acessada por uma Thread de cada vez.  

Já o Semáforo genérico pode ser usado quando existem vários recursos iguais e um número limitado de threads pode acessar o recurso ao mesmo tempo.

**5)**  Os possíveis valores finais da variável são 9, 10 e 11.

**6)** Região crítica é o trecho do programa que acessa recursos compartilhados e que não pode ser executado simultaneamente por várias tarefas. Ela é importante porque, sem proteção adequada, ocorrem condições de corrida, inconsistência de dados e outros problemas típicos da programação concorrente.

**7)**