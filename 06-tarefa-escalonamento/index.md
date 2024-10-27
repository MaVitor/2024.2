# Escalonamento de tarefas

## Informações gerais

- Capítulo: [Escalonamento de tarefas](https://wiki.inf.ufpr.br/maziero/lib/exe/fetch.php?media=socm:socm-06.pdf)
- Disciplina: *sistemas operacionais*
- Livro: [Sistemas Operacionais: Conceitos e Mecanismos](https://wiki.inf.ufpr.br/maziero/doku.php?id=socm:start)

## Aluno

- nome: Mateus Vitor Cavalcanti Rodrigues
- matrícula: 20232014040031

## Respostas dos exercícios

**1. Explique o que é escalonamento round-robin, dando um exemplo.**
O escalonamento round-robin é um algoritmo preemptivo que distribui o tempo de processador entre todas as tarefas prontas, atribuindo a cada uma um quantum de tempo. Se a tarefa não terminar nesse intervalo, ela volta para o fim da fila de tarefas prontas, e o processador é atribuído à próxima tarefa. Por exemplo, com três tarefas t1, t2 e t3 e um quantum de 2 segundos, o processador executaria t1 por 2 segundos, depois t2 por 2 segundos, seguido de t3, retornando a t1 após todas as tarefas terem tido uma chance de executar.

**2. Considere um sistema de tempo compartilhado com valor de quantum tq e duração da troca de contexto ttc. Considere tarefas de entrada/saída que usam em média p% de seu quantum de tempo cada vez que recebem o processador. Defina a eficiência E do sistema como uma função dos parâmetros tq, ttc e p.**
A eficiência E do sistema pode ser definida como a fração do tempo em que o processador é utilizado para executar as tarefas, em vez de realizar trocas de contexto. A fórmula para a eficiência seria:
E = (p * tq) / (p * tq + ttc)
Ou seja, quanto maior for o valor de p e de tq em relação ao tempo de troca de contexto ttc, maior será a eficiência.

**3. Explique o que é, para que serve e como funciona a técnica de aging.**
A técnica de aging é usada para evitar que tarefas de baixa prioridade "morram de fome" em sistemas de escalonamento por prioridade. Ela funciona aumentando a prioridade de uma tarefa à medida que ela permanece na fila de prontas sem ser executada. Quanto mais tempo a tarefa espera, mais sua prioridade aumenta, permitindo que eventualmente ela receba o processador. Isso garante que todas as tarefas tenham uma chance de executar, mesmo em sistemas com muitas tarefas de alta prioridade.

**4. No algoritmo de envelhecimento definido na Seção 6.4.6, o que seria necessário modificar para suportar uma escala de prioridades negativa?**
Para suportar uma escala de prioridades negativa, seria necessário alterar a função de envelhecimento para diminuir a prioridade ao longo do tempo, em vez de aumentá-la. Isso garantiria que quanto mais tempo uma tarefa ficasse na fila de prontas, menor seria seu valor de prioridade negativa, aumentando suas chances de ser escolhida.

**5. A tabela a seguir representa um conjunto de tarefas prontas para utilizar um processador:**
Tarefa t1 | t2 | t3 | t4 | t5
Ingresso 0 | 0 | 3 | 5 | 7
Duração 5 | 4 | 5 | 6 | 4
Prioridade 2 | 3 | 5 | 9 | 6

Represente graficamente a sequência de execução das tarefas e calcule os tempos médios de vida (tournaround time) e de espera (waiting time), para as políticas de escalonamento a seguir:**

(a) FCFS cooperativa
Na política FCFS, as tarefas são executadas na ordem de chegada. A sequência seria: t1 → t2 → t3 → t4 → t5. O tempo médio de vida (turnaround time) e o tempo de espera (waiting time) podem ser calculados com base na ordem de execução.

(b) SJF cooperativa
No SJF cooperativo, as tarefas mais curtas são executadas primeiro. A sequência seria: t2 → t5 → t1 → t3 → t4.

(c) SJF preemptiva (SRTF)
Na SJF preemptiva, uma nova tarefa mais curta pode interromper a execução de uma tarefa em andamento. A sequência mudaria conforme as novas tarefas mais curtas entram no sistema.

(d) PRIO cooperativa
No PRIO cooperativo, a tarefa com maior prioridade é executada primeiro. A sequência seria: t4 → t5 → t3 → t2 → t1.

(e) PRIO preemptiva
No PRIO preemptivo, uma tarefa de maior prioridade pode interromper uma tarefa em andamento. A sequência seria ajustada conforme tarefas mais prioritárias entram no sistema.

(f) RR com tq = 2, sem envelhecimento
No Round-Robin, as tarefas são executadas por quanta de 2 segundos. A sequência seria: t1 → t2 → t3 → t4 → t5 com revezamento entre as tarefas conforme seus tempos de execução.

**6. Idem, para as tarefas da tabela a seguir:**
Tarefa t1 | t2 | t3 | t4 | t5
Ingresso 0 | 0 | 1 | 7 | 11
Duração 5 | 6 | 2 | 6 | 4
Prioridade 2 | 3 | 4 | 7 | 9

A sequência de execução e os tempos de turnaround e espera podem ser calculados para cada política de escalonamento listada acima, considerando a ordem de ingresso, duração e prioridade das tarefas.