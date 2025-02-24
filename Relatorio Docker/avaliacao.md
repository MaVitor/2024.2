# Docker Compose com Django e Banco de Dados

## Informações Gerais

- Assunto: Docker, containerizar aplicativos
- Disciplina: *Sistemas Operacionais*

## Relatório

### Aluno

- Nome: Mateus Vitor Cavalcanti Rodrigues
- Matrícula: 20232014040031

### Relato

Para realizar a atividade proposta, foi criada uma branch denominada *docker* no repositório do PDS Web Bizzu. Nessa branch, foram adicionados dois arquivos principais: o *Dockerfile* e o *docker-compose.yml*. 

Primeiramente, no arquivo *Dockerfile*, foi configurado um código responsável por criar a imagem da aplicação, usando a imagem base do Python. Além disso, dentro desse container, foi criada uma pasta chamada `/bizzu` e todas as dependências especificadas no arquivo *requirements.txt* foram instaladas. No entanto, com isso, apenas a imagem foi criada, mas a execução da aplicação não foi realizada. Para resolver isso, criamos o arquivo *docker-compose.yml*, que possibilita a execução do container ao configurar um serviço.

Dentro desse serviço, foram feitas algumas configurações para garantir que a aplicação fosse executada corretamente, como:
- **Build**: Define o caminho para o *Dockerfile* a ser utilizado na construção da imagem. Como o *Dockerfile* está no mesmo diretório, utilizamos o `.`.
- **Command**: Especifica o comando que precisa ser executado para rodar a aplicação. Usamos o comando `bash -c` para concatenar dois comandos: o de migração do banco de dados e o de execução do servidor. Isso é necessário porque, geralmente, ao rodar uma aplicação Django, precisamos executar esses dois comandos.
- **Ports**: Mapeia a porta da aplicação para a porta do container, permitindo a comunicação entre eles.

Para configurar o banco de dados, foi necessário modificar o arquivo de *settings.py* para usar o PostgreSQL no lugar do SQLite. Para isso, adicionamos um novo serviço no *docker-compose.yml* e fizemos as devidas configurações, incluindo:
- **container_name**: Atribui um nome ao container que armazenará o banco de dados.
- **ports**: Mapeia a porta do container para a porta do banco de dados.
- **image**: Define a imagem do PostgreSQL que será utilizada.
- **environment**: Adiciona variáveis de ambiente para configurar a conexão com o banco, como usuário e senha.
- **Volumes**: Define o local onde as informações persistentes do banco serão armazenadas.

Com essas modificações, criamos um novo serviço chamado *DB*, que hospeda o banco de dados PostgreSQL em um container. 

Não foi necessário criar um *Dockerfile* adicional para o PostgreSQL, pois ele já possui uma imagem oficial que pode ser utilizada diretamente sem a necessidade de personalizações.

### Arquivos Docker e Configuração do Django

Como os arquivos não são compatíveis com Markdown, eles estão localizados no mesmo diretório em que este relatório foi salvo. O nome dos arquivos indica claramente o que eles contêm: o *Dockerfile* é o arquivo de configuração do Docker e o *settings.py* contém as configurações específicas do nosso projeto Django.
