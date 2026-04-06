
### Nome: Gabriel Augusto de Lima Maia

**1a)** Aqui, estamos usando a fase de pré processamento, e criando um novo arquivo fonte em C pronto para compilação.

**b)** Aqui estamos na fase de compilação, e transformando esse código pre-processado em um arquivo assembly.

**c)** Aqui, estamos usando programa assembler e transformando o código em código de maquina na fase de montagem, resultando em um arquivo objeto.

**d)** Já aqui é a fase de ligação, o linker junta o arquivo com outras bibliotecas que são necessárias para o funcionamento do código e ai gera o arquivo executável.

**2a)** Linguagens interpretadas são de execução imediata, já que o interpretador é um programa que executa passos de uma linguagem, então não é necessário compilar e executar os arquivos. Porém isso torna os interpretadores mais lento, já que o interpretador tem que rodar em tempo de execução. Um exemplo é python.

**b)** Linguagens interpretadas que também são maquinas virtuais, tem como vantagem a portabilidade e maior segurança, elas podem rodar em diferentes arquiteturas e o programa é isolado em relação ao sistema. Porém tem um consumo extra de memoria e processamento por causa dessa camada extra e tem um desempenho menor comparado a código puro. Um exemplo de linguagem é java(JVM).

**c)** Múltiplos programas compartilham uma cópia de funções de biblioteca, as bibliotecas podem ser atualizadas independentemente dos programas e podem evitar carregar códigos que não são executáveis. Porém pode gerar erros que não são fáceis de rastrear se a dependência não estiver disponível e também criar mais um ciclo de execução que custa tempo. Java é um linguagem que usa ligação tardia.

**d)** Permite medir o desempenho do programa e encontrar gargalos e também ajuda a entender o uso de memoria, tempo de execução e chamada de funções. Porém adiciona mais overhead, fazendo o programa rodar mais lento durante a instrumentação. Um exemplo de linguagem que da para utilizar instrumentação é C, que tem a ferramenta gprof no gcc.

**e)** ao compilar trechos de códigos que ocorrem repetidamente, ela aumenta o desempenho do programa, otimizando esses trechos. A desvantagem é que uma implementação mais complexa e que consome tempo e memoria extra na inicialização. O java utiliza Compilação dinâmica.

**3a)** o que foi impresso é: Result = 1234.

**b)** O programa gerado é B8 34 12 00 00 C3, que em assembly faz 

``` assembly
mov eax, 0x1234;
ret;
```
e esse programa é armazenado no buffer.

**c)** Não, esse conjunto específico de instruções em bytes só faz sentido em x86/x86-64.

**4a)** O register é uma sugestão ao compilador para guardar uma variável em um registrador da cpu em vez da memoria, uma vez que a leitura aos registradores é mais rápido do que na memoria.

**Exemplo:**

```c
#include <stdio.h>

int soma_array(int *arr, int n) {
    register int i;     // sugestão: usar registrador para 'i'
    register int soma = 0; // sugestão: 'soma' em registrador também

    for (i = 0; i < n; i++) {
        soma += arr[i];
    }

    return soma;
}

int main() {
    int valores[5] = {1, 2, 3, 4, 5};
    printf("Soma = %d\n", soma_array (valores,5));
    return 0;
}

```

**b)** o Inline também é uma sugestão ao compilador, ele sugere que uma função deve ser expandida no lugar da chamada, isso evita o custo de uma chamada de função.

**Exemplo:**

```cpp
#include <iostream>
using namespace std;

// Sugestão ao compilador: expandir inline
inline int quadrado(int x) {
    return x * x;
}

int main() {
    int a = 5;
    int b = quadrado(a); // pode ser substituído diretamente por "a * a"
    cout << "Quadrado de " << a << " = " << b << endl;
    return 0;
}

```

**5a)** O crescimento acontece porque a flag -g adiciona mais informações de depuração no binário, como nome de variáveis, endereços de linhas e contexto das informações, assim fica mais fácil para o gdb de fazer a ponte entre o código fonte e o código de maquina.

**b)**
Com comentário:
```bash
==8509== Memcheck, a memory error detector
==8509== Copyright (C) 2002-2022, and GNU GPLd, by Julian Seward et al.
==8509== Using Valgrind-3.22.0 and LibVEX; rerun with -h for copyright info
==8509== Command: ./sla
==8509== 
3
==8509== 
==8509== HEAP SUMMARY:
==8509==     in use at exit: 4 bytes in 1 blocks
==8509==   total heap usage: 2 allocs, 1 frees, 1,028 bytes allocated
==8509== 
==8509== LEAK SUMMARY:
==8509==    definitely lost: 4 bytes in 1 blocks
==8509==    indirectly lost: 0 bytes in 0 blocks
==8509==      possibly lost: 0 bytes in 0 blocks
==8509==    still reachable: 0 bytes in 0 blocks
==8509==         suppressed: 0 bytes in 0 blocks
==8509== Rerun with --leak-check=full to see details of leaked memory
==8509== 
==8509== For lists of detected and suppressed errors, rerun with: -s
==8509== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

sem comentario:

```bash
==8748== Memcheck, a memory error detector
==8748== Copyright (C) 2002-2022, and GNU GPLd, by Julian Seward et al.
==8748== Using Valgrind-3.22.0 and LibVEX; rerun with -h for copyright info
==8748== Command: ./sla
==8748== 
3
==8748== 
==8748== HEAP SUMMARY:
==8748==     in use at exit: 0 bytes in 0 blocks
==8748==   total heap usage: 2 allocs, 2 frees, 1,028 bytes allocated
==8748== 
==8748== All heap blocks were freed -- no leaks are possible
==8748== 
==8748== For lists of detected and suppressed errors, rerun with: -s
==8748== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```
**6)**

float j = 3.2;
j = j - 1.7;

-  Amarração de tempo de compilação, ao associar a variável j ao tipo float.
- Tempo de carga, quando é decido qual endereço de memoria a variável j fica.
- Tempo de execução, quando a variável j recebe o valor 3.2 e depois 1.
- Tempo de implementação, quando o compilador decide o tamanho do float
- Tempo de projeto, quando os projetistas da linguagem decidiram que o simbolo - significa subtração.
  
**7a)** Nesse exemplo em php, o tipo é declarado em tempo de execução porque a variável não é declarada de forma explicita.
**b)** Já nesse exemplo em c#, o tipo declarado é em tempo de compilação, já que declaramos o tipo da variável e o compilador sabe que int x é um inteiro antes de rodar o programa.

**8a)** 
