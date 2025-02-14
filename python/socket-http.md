# Tutorial: Criando um Servidor TCP Simples em Python

## Informações gerais
- **Público alvo**: alunos da disciplina de SO (Sistemas Operacionais) do curso de TADS (Superior em Tecnologia em Análise e Desenvolvimento de Sistemas) no CNAT-IFRN (Instituto Federal de Educação, Ciência e Tecnologia do Rio Grande do Norte - Campus Natal-Central).
- **Disciplina**: Sistemas Operacionais (SO)
- **Professor**: [Leonardo A. Minora](https://github.com/leonardo-minora)
- **Texto gerado pelo**: [Microsoft Copilot](https://copilot.microsoft.com/)

## Sumário
1. Servidor TCP sem thread
2. Experimento 1 - usando thread no servidor
3. Experimento 2 - usando containers

---

## 1. Servidor TCP sem thread
Este tutorial apresenta um servidor TCP básico sem uso de threads, explicando sua implementação e comportamento ao lidar com várias conexões simultâneas.

### Passos para executar o experimento:
1. Criar e executar o servidor TCP sem thread.
2. Criar e executar o cliente TCP para se conectar ao servidor.
3. Testar com diferentes quantidades de clientes simultâneos (1, 2, 5 e 10 clientes).
4. Observar e documentar o comportamento do servidor ao receber múltiplas conexões.

### Implementação do Servidor TCP Sem Thread
```python
import socket

HOST = ""  # Endereço IP do servidor (vazio para aceitar conexões de qualquer endereço)
PORT = 8000  # Porta do servidor

# Criando o socket do servidor
servidor = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
servidor.bind((HOST, PORT))
servidor.listen(1)

print(f"Servidor TCP rodando na porta {PORT}...")

while True:
    conexao, endereco = servidor.accept()
    print(f"Conexão estabelecida com {endereco}")
    mensagem = "Olá, cliente! Você está conectado ao servidor TCP."
    conexao.sendall(mensagem.encode("utf-8"))
    conexao.close()
```

---

## 2. Experimento 1 - Uso de Threads no Servidor
Neste experimento, analisaremos o desempenho do servidor sem e com threads, comparando os tempos de resposta em diferentes cenários.

### Passos do Experimento
1. Executar o servidor sem thread.
2. Executar o cliente TCP para testar com:
   - 1 cliente
   - 2 clientes simultâneos
   - 5 clientes simultâneos
   - 10 clientes simultâneos
3. Analisar e explicar o comportamento do servidor sem thread.
4. Parar o servidor sem thread e executar a versão com thread.
5. Repetir os testes com diferentes quantidades de clientes.
6. Comparar e discutir as diferenças observadas.

### Implementação do Servidor TCP com Thread
```python
import socket
import threading

HOST = ""
PORT = 8000

# Criando o socket do servidor
servidor = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
servidor.bind((HOST, PORT))
servidor.listen(5)

print(f"Servidor TCP multithread rodando na porta {PORT}...")

def atender_cliente(conexao, endereco):
    print(f"Conexão estabelecida com {endereco}")
    mensagem = "Olá, cliente! Você está conectado ao servidor TCP multithread."
    conexao.sendall(mensagem.encode("utf-8"))
    conexao.close()

while True:
    conexao, endereco = servidor.accept()
    thread = threading.Thread(target=atender_cliente, args=(conexao, endereco))
    thread.start()
```

### Implementação do Cliente TCP
```python
import socket

def fazer_requisicao():
    cliente = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    cliente.connect(("localhost", 8000))
    resposta = cliente.recv(1024)
    print("Resposta do servidor:", resposta.decode("utf-8"))
    cliente.close()

fazer_requisicao()
```

---

## 3. Experimento 2 - Uso de Containers
Neste experimento, usaremos Docker para executar o servidor TCP em um container, avaliando o impacto no desempenho e na gestão de processos.

### Passos do Experimento
1. Criar um `Dockerfile` para o servidor TCP.
2. Construir a imagem Docker.
3. Executar o container do servidor.
4. Testar a acessibilidade do servidor dentro e fora do container.
5. Comparar o desempenho do servidor em ambiente nativo e em container.

### Implementação do Dockerfile
Crie um arquivo chamado `Dockerfile` e adicione o seguinte conteúdo:
```dockerfile
# Usar imagem base do Python
FROM python:3.9

# Copiar o código do servidor para o container
COPY servidor.py /servidor.py

# Definir o diretório de trabalho
WORKDIR /

# Comando para executar o servidor
CMD ["python", "servidor.py"]
```

### Construção e Execução do Container
1. **Construir a imagem**:
   ```sh
   docker build -t servidor-tcp .
   ```
2. **Executar o container**:
   ```sh
   docker run -p 8000:8000 servidor-tcp
   ```
3. **Testar o servidor**:
   - Execute o cliente TCP para conectar ao servidor dentro do container.

### Conclusão
O uso de threads melhora a capacidade do servidor de lidar com múltiplos clientes simultaneamente. A execução em containers facilita a distribuição e a escalabilidade, mas pode introduzir uma pequena latência devido à abstração do ambiente.

---

## Links
- [socket — Low-level networking interface](https://docs.python.org/3/library/socket.html)

