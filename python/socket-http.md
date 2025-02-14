# Tutorial: Criando um Servidor TCP Simples em Python

## Informações Gerais
- **Público-alvo**: Alunos da disciplina de Sistemas Operacionais (SO) do curso de TADS no CNAT-IFRN.
- **Disciplina**: Sistemas Operacionais (SO)
- **Professor**: [Leonardo A. Minora](https://github.com/leonardo-minora)
- **Texto gerado pelo**: [Microsoft Copilot](https://copilot.microsoft.com/)

## Sumário
1. Introdução
2. Servidor TCP sem thread
3. Experimento 1 - Uso de Threads no Servidor
4. Experimento 2 - Uso de Containers
5. Comparativo de Desempenho
6. Conclusão

---

## 1. Introdução
Este tutorial apresenta a implementação e a análise de um servidor TCP básico, explorando diferentes abordagens para lidar com múltiplas conexões simultâneas. Serão abordadas três formas de execução:
- Servidor TCP sem threads.
- Servidor TCP com threads.
- Servidor TCP executando em containers Docker.

O objetivo é compreender as vantagens e limitações de cada abordagem e avaliar seu desempenho.

---

## 2. Servidor TCP sem Thread
Nesta primeira abordagem, o servidor processa uma conexão por vez, sem suporte para múltiplas conexões simultâneas.

### Passos para executar o experimento:
1. Criar e executar o servidor TCP sem thread.
2. Criar e executar o cliente TCP para se conectar ao servidor.
3. Testar com diferentes quantidades de clientes simultâneos (1, 2, 5 e 10 clientes).
4. Observar e documentar o comportamento do servidor ao receber múltiplas conexões.

### Implementação do Servidor TCP Sem Thread
```python
import socket

HOST = ""
PORT = 8000

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

## 3. Experimento 1 - Uso de Threads no Servidor
Neste experimento, implementamos um servidor que usa threads para lidar com múltiplas conexões simultâneas.

### Passos do Experimento:
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

---

## 4. Experimento 2 - Uso de Containers
Neste experimento, utilizamos Docker para executar o servidor TCP dentro de um container.

### Passos do Experimento:
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

---

## 5. Comparativo de Desempenho
| Modo de Execução | Tempo de Resposta (médio) | Suporte a Clientes Simultâneos |
|-------------------|--------------------|----------------------------|
| Sem Thread       | Alto               | Baixo                      |
| Com Thread      | Médio              | Alto                       |
| Em Container     | Variável           | Alto                       |

- **Servidor Sem Thread**: Rápido para conexões individuais, mas sofre com múltiplos clientes.
- **Servidor com Thread**: Melhor para múltiplas conexões simultâneas.
- **Servidor em Container**: Oferece flexibilidade e escalabilidade, mas pode ter pequena latência.

---

## 6. Conclusão
O uso de threads melhora significativamente a capacidade do servidor de lidar com múltiplos clientes. A execução em containers é útil para distribuição e escalabilidade, embora introduza um pequeno overhead. A escolha da abordagem depende do cenário e dos requisitos da aplicação.

---

## Links
- [socket — Low-level networking interface](https://docs.python.org/3/library/socket.html)

