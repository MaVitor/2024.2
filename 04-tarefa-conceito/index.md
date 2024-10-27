# Conceito de tarefas

## Informações gerais

- Capítulo: [Conceito de tarefas](https://wiki.inf.ufpr.br/maziero/lib/exe/fetch.php?media=socm:socm-04.pdf)
- Disciplina: *sistemas operacionais*
- Livro: [Sistemas Operacionais: Conceitos e Mecanismos](https://wiki.inf.ufpr.br/maziero/doku.php?id=socm:start)

## Aluno

- nome: Mateus Vitor Cavalcanti Rodrigues
- matrícula: 20232014040031

## Respostas dos exercícios

**1. O que significa time sharing e qual a sua importância em um sistema operacional?**

**Time sharing é uma técnica em que o processador compartilha seu tempo entre várias tarefas, atribuindo fatias de tempo (quantum) a cada uma. Isso permite que várias tarefas sejam executadas de maneira aparentemente simultânea, aumentando a eficiência do sistema, especialmente em ambientes multitarefa. A importância do time sharing está em garantir que todos os usuários e processos recebam uma parcela justa do processamento, evitando que um único processo monopolize o sistema.**

**2. Como e com base em que critérios é escolhida a duração de um quantum de processamento?**

A duração do quantum de processamento é escolhida com base em um equilíbrio entre a responsividade do sistema e a eficiência do uso do processador. Se o quantum for muito curto, o sistema gastará muito tempo trocando de tarefas (overhead). Se for muito longo, a interatividade do sistema será prejudicada, pois as tarefas terão que esperar muito para serem executadas novamente. A escolha do quantum pode depender do tipo de aplicação, da prioridade da tarefa e das características do sistema.

**3. Complete o diagrama com a transição de estado que está faltando (t6) e apresente o significado de cada um dos estados e transições.**

A transição t6 que está faltando no diagrama é a transição de "S" (suspensa) para "P" (pronta). Essa transição ocorre quando o evento ou recurso que a tarefa estava aguardando se torna disponível, permitindo que ela retorne à fila de tarefas prontas para serem executadas.

**4. Indique se cada uma das transições de estado de tarefas a seguir definidas é possível ou não.**

E→ P: Possível. Ocorre quando o quantum de tempo da tarefa se esgota, e ela volta para a fila de prontas.

E→ S: Possível. Acontece quando a tarefa precisa esperar por um recurso, como uma operação de entrada/saída.

S→ E: Possível. Quando o recurso que a tarefa aguardava fica disponível, ela pode ser retomada.

P→ N: Não é possível. Uma tarefa já criada não pode voltar ao estado de nova.

S→ T: Possível. Ocorre se uma tarefa suspensa for encerrada ou abortada.

E→ T: Possível. Ocorre quando a tarefa termina sua execução ou é encerrada.

N→ S: Não é possível. A tarefa deve estar pronta ou executando antes de ser suspensa.

P→ S: Possível. Quando uma tarefa pronta aguarda por um recurso antes de executar, ela pode ser suspensa.

**5. Relacione as afirmações abaixo aos respectivos estados no ciclo de vida das tarefas.**

[N] O código da tarefa está sendo carregado.

[P] As tarefas são ordenadas por prioridades.

[S] A tarefa sai deste estado ao solicitar uma operação de entrada/saída.

[T] Os recursos usados pela tarefa são devolvidos ao sistema.

[P] A tarefa vai a este estado ao terminar seu quantum.

[P] A tarefa só precisa do processador para poder executar.

[S] O acesso a um semáforo em uso pode levar a tarefa a este estado.

[E] A tarefa pode criar novas tarefas.

[E] Há uma tarefa neste estado para cada processador do sistema.

[S] A tarefa aguarda a ocorrência de um evento externo