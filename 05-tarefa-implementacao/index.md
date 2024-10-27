# Implementação de tarefas

## Informações gerais

- Capítulo: [Implementação de tarefas](https://wiki.inf.ufpr.br/maziero/lib/exe/fetch.php?media=socm:socm-05.pdf)
- Disciplina: *sistemas operacionais*
- Livro: [Sistemas Operacionais: Conceitos e Mecanismos](https://wiki.inf.ufpr.br/maziero/doku.php?id=socm:start)

## Aluno

- nome: Mateus Vitor Cavalcanti Rodrigues
- matrícula: 20232014040031

## Respostas dos exercícios

**1. Explique o que é, para que serve e o que contém um TCB - Task Control Block.**
O TCB (Task Control Block) é uma estrutura de dados usada pelo sistema operacional para armazenar as informações necessárias à gestão de uma tarefa (ou processo). Ele contém o contexto da tarefa (valores dos registradores, ponteiros de pilha, etc.), seu estado atual (pronta, executando, suspensa), identificadores, recursos utilizados (arquivos abertos, conexões de rede) e informações de prioridade e contabilização. Serve para permitir que o sistema operacional suspenda e retome tarefas de forma eficiente e transparente.

**2. Desenhe o diagrama de tempo da execução do código a seguir, informe qual a saída do programa na tela (com os valores de x) e calcule a duração aproximada de sua execução.**
O diagrama de tempo do código inclui duas chamadas para fork(), que criam processos filhos. O valor de x é incrementado duas vezes em cada processo, resultando em múltiplas impressões com diferentes valores de x. Considerando os sleep(5) no código, a execução total deve durar aproximadamente 10 segundos. O valor final de x depende de quantas vezes o código é executado nos processos pai e filhos. A saída incluirá várias linhas com "Valor de x: 1" e "Valor de x: 2", de acordo com a quantidade de processos criados.

**3. Indique quantas letras “X” serão impressas na tela pelo programa abaixo.**
O programa imprime "X" uma vez para cada processo criado com fork(). Considerando a linha de comando a.out 4 3 2 1, o programa cria N processos adicionais com base no valor de N. Assim, ao todo, a tela exibirá várias letras "X", sendo o número exato resultado da quantidade de processos criados pelos fork() e suas condições.

**4. O que são threads e para que servem?**
Threads são fluxos de execução independentes dentro de um processo. Elas servem para permitir que diferentes partes de um programa sejam executadas simultaneamente, compartilhando o mesmo espaço de memória e recursos do processo. Isso é útil para aumentar a eficiência em tarefas paralelas, como a manipulação de várias conexões de rede simultaneamente em um servidor.

**5. Quais as principais vantagens e desvantagens de threads em relação a processos?**
Vantagens: Threads são mais leves que processos, compartilham recursos como memória e arquivos abertos, e a troca de contexto entre threads é mais rápida.
Desvantagens: Threads têm menor robustez, já que um erro em uma thread pode afetar outras threads no mesmo processo. Além disso, todas as threads de um processo compartilham as mesmas permissões e recursos, o que pode ser menos seguro.

**6. Forneça dois exemplos de problemas cuja implementação multi-thread não tem desempenho melhor que a respectiva implementação sequencial.**
Exemplo 1: Processos que realizam cálculos intensivos e não precisam interagir com dispositivos de entrada/saída podem não se beneficiar do uso de threads, já que o overhead de gerenciamento das threads pode aumentar o tempo total de execução.
Exemplo 2: Aplicações que dependem fortemente de recursos compartilhados, como arquivos, podem sofrer contenção de recursos, resultando em threads bloqueando umas às outras e, consequentemente, sem ganho de desempenho.

**7. Associe as afirmações a seguir aos seguintes modelos de threads: a) many-to-one (N:1); b) one-to-one (1:1); c) many-to-many (N).**

(a) a. Tem a implementação mais simples, leve e eficiente.

(b) c. Multiplexa os threads de usuário em um pool de threads de núcleo.

(c) b. Pode impor uma carga muito pesada ao núcleo.

(d) a. Não permite explorar a presença de várias CPUs pelo mesmo processo.

(e) c. Permite uma maior concorrência sem impor muita carga ao núcleo.

(f) a. Geralmente implementado por bibliotecas.

(g) b. É o modelo implementado no Windows NT e seus sucessores.

(h) a. Se um thread bloquear, todos os demais têm de esperar por ele.

(i) b. Cada thread no nível do usuário tem sua correspondente dentro do núcleo.

(j) c. É o modelo com implementação mais complexa.

**8. Considerando as implementações de threads N:1 e 1:1 para o trecho de código a seguir**

**a) desenhe os diagramas de execução**

**b) informe as durações aproximadas de execução**

**c) indique a saída do programa na tela.**

Na implementação N:1, todas as threads são gerenciadas em nível de usuário, portanto apenas uma thread executa por vez. Na implementação 1:1, o sistema operacional gerencia as threads, permitindo que várias threads executem em paralelo. A duração da execução na implementação N:1 será maior devido à falta de paralelismo, enquanto na implementação 1:1 a execução será mais rápida. A saída exibirá os valores de x e y de acordo com a ordem de execução das threads e a sincronização dos valores compartilhados.