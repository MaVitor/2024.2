# Arquiteturas de Sistemas Operacionais

## Informações gerais

- Capítulo: [Arquitetura de SO](https://wiki.inf.ufpr.br/maziero/lib/exe/fetch.php?media=socm:socm-03.pdf)
- Disciplina: *sistemas operacionais*
- Livro: [Sistemas Operacionais: Conceitos e Mecanismos](https://wiki.inf.ufpr.br/maziero/doku.php?id=socm:start)

## Aluno

- nome: Mateus Vitor Cavalcanti Rodrigues
- matrícula: 20232014040031

## Respostas dos exercícios

**1. Tabela com benefícios e deficiências das principais arquiteturas de sistemas operacionais:**

Arquitetura | Benefícios | Deficiências

Monolítica | Alto desempenho, acesso direto aos componentes do sistema, simplicidade na implementação inicial | Baixa modularidade, complexidade na manutenção, erros podem afetar o sistema inteiro

Micronúcleo | Maior modularidade, flexibilidade, robustez (falhas afetam apenas o serviço correspondente) | Menor desempenho devido ao uso intenso de troca de mensagens

Em Camadas | Organização estruturada, facilita manutenção e atualização | Redução de desempenho, dificuldade em separar algumas funcionalidades interdependentes

Híbrida | Combina vantagens do monolítico e do micronúcleo, melhora o desempenho sem perder modularidade | Complexidade no design, pode misturar características conflitantes

Máquinas Virtuais | Permite execução de múltiplos sistemas simultaneamente, isolamento e segurança | Desempenho reduzido em relação à execução nativa, dependência do hipervisor

Contêineres | Isolamento de processos em um único SO, gerenciamento eficiente de recursos | Menos seguro que hipervisores de sistema, dependente de um único núcleo compartilhado

Exonúcleo | Alto desempenho, cada aplicação pode implementar abstrações personalizadas | Complexidade no desenvolvimento, sem abstrações padrão de SO

Uninúcleo | Alta eficiência, ideal para ambientes de nuvem, sistema compacto | Menos flexível, dificilmente reaproveitável para outras aplicações

**2. O Linux possui um núcleo similar com o da figura 3.1, mas também possui “tarefas de núcleo” que executam como os gerentes da figura 3.2. Seu núcleo é monolítico ou micronúcleo? Por quê?**

O Linux é considerado um sistema monolítico. Embora possua "tarefas de núcleo" semelhantes aos gerentes de sistemas micronúcleo, seu design permite que todos os componentes do núcleo interajam diretamente, sem a necessidade de troca de mensagens. Esse acesso direto contribui para o alto desempenho do sistema, uma característica das arquiteturas monolíticas.

**3. Sobre as afirmações a seguir, relativas às diversas arquiteturas de sistemas operacionais, indique quais são incorretas, justificando sua resposta:**

a) Incorreta. Uma máquina virtual de sistema permite a execução de um sistema operacional completo, enquanto máquinas virtuais de aplicação suportam uma única aplicação em uma linguagem específica, como Java.

b) Correta. Um hipervisor convidado executa sobre um sistema operacional hospedeiro.

c) Incorreta. Em sistemas micronúcleo, os componentes são implementados fora do núcleo, em processos separados que se comunicam por troca de mensagens, e não como módulos interconectados no núcleo.

d) Incorreta. Núcleos monolíticos não são conhecidos por sua robustez e facilidade de manutenção; ao contrário, sua manutenção pode ser complexa e uma falha em um módulo pode comprometer o sistema inteiro.

e) Correta. Em sistemas micronúcleo, as chamadas de sistema são implementadas por meio de trocas de mensagens, devido à separação dos serviços do núcleo.

