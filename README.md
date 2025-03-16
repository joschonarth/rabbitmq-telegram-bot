# 🐇 Integração RabbitMQ com Telegram Bot 📲

Este projeto integra o **RabbitMQ** com a API do Telegram, permitindo o envio automatizado e eficiente de mensagens diretamente para usuários ou grupos no Telegram, com a utilização de filas de mensagens para garantir a comunicação assíncrona e escalável.

## 🛠️ Tecnologias Utilizadas

- 🐍 **Python**: Linguagem de programação usada para desenvolver a lógica do projeto.
- 🐇 **RabbitMQ**: Sistema de mensagens de código aberto que permite o envio e recebimento de mensagens entre sistemas distribuídos de forma assíncrona.
- 📦 **Pika**: Biblioteca Python para interagir com o RabbitMQ, permitindo a publicação e o consumo de mensagens de maneira simples.
- 🤖 **Telegram Bot**: Utilizado para enviar mensagens automatizadas do sistema para os usuários no Telegram, utilizando a API do Telegram.
- 🌱 **dotenv**: Biblioteca que facilita o carregamento de variáveis de ambiente de um arquivo `.env`, garantindo maior segurança e flexibilidade no projeto.
- 🌐 **requests**: Biblioteca para facilitar o envio de requisições HTTP, essencial para a comunicação com APIs externas, como o Telegram.

## ⚙️ Configuração do Ambiente

1. **Clone o repositório:**

   ```bash
   git clone https://github.com/joschonarth/rabbitmq-telegram-bot.git
   cd rabbitmq-telegram-bot
   ```

2. **Crie um ambiente virtual (opcional):**

   ```bash
   python -m venv venv
   source venv/bin/activate  # No Windows: venv\Scripts\activate
   ```

3. **Instale as dependências:**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure as variáveis de ambiente:**

   O projeto inclui um arquivo `.env.example` com exemplos das variáveis de ambiente necessárias. Copie esse arquivo para `.env` usando o comando:

   ```bash
   cp .env.example .env
   ```

   Edite o arquivo `.env` para configurar as variáveis de ambiente necessárias.

## 📦 Configuração do RabbitMQ

Certifique-se de ter o **RabbitMQ** instalado e em execução. Para subir a imagem do **RabbitMQ** no **Docker**, basta executar o `docker-compose`:

```bash
docker-compose up -d
```

O **RabbitMQ** será iniciado em segundo plano. Acesse o painel do **RabbitMQ** em [http://localhost:15672/](http://localhost:15672/) (usuário: `guest`, senha: `guest`).

## 🔧 Configuração do Telegram Bot

### 🤖 Como obter o **Token do bot do Telegram**

1. Abra o Telegram e pesquise por **BotFather**.
2. Inicie uma conversa com o **BotFather** e envie o comando `/newbot` para criar um novo bot.
3. O **BotFather** pedirá que você forneça um nome e um nome de usuário para o bot.
4. Após a criação, ele fornecerá o **Token** do bot. Copie esse token e defina a variável de ambiente `TELEGRAM_TOKEN` com o valor obtido.

---

### 📱 Como obter o **ID do chat ou grupo**

#### Para obter o **ID do chat pessoal**:

1. Acesse a URL: `https://api.telegram.org/bot<SEU_TOKEN>/getUpdates` (substitua `<SEU_TOKEN>` pelo seu token).
2. Envie uma mensagem para o seu bot no Telegram.
3. Acesse a resposta da API e localize o campo `"chat"`, onde você encontrará o `chat_id`. Defina esse valor na variável de ambiente `TELEGRAM_CHAT_ID`.

#### Para um **ID de grupo**:

1. Adicione o bot ao grupo do Telegram.
2. Envie uma mensagem no grupo.
3. Acesse a URL novamente: `https://api.telegram.org/bot<SEU_TOKEN>/getUpdates` e localize o `chat_id` referente ao grupo.
4. Defina o valor obtido na variável de ambiente `TELEGRAM_CHAT_ID`.

## 🚀 Execução do Projeto

### 📤 Publisher (Envia mensagens para a fila do RabbitMQ)

A mensagem a ser enviada fica dentro do arquivo `publisher.py`. Você pode modificar o conteúdo da mensagem dentro do arquivo conforme necessário.

```python
rabbit_mq_publisher.send_message({ "message": "Sua mensagem" })
```

Execute o `publisher.py` com o comando abaixo para enviar uma mensagem:

```bash
python publisher.py
```

### 📥 Consumer (Lê mensagens da fila e envia pelo Telegram)

O arquivo `consumer.py` é responsável por consumir as mensagens da fila do RabbitMQ e enviá-las para o Telegram. Quando executado, ele aguarda as mensagens na fila e, ao receber uma mensagem, envia automaticamente para o chat do Telegram configurado.

Execute o `consumer.py` com o comando abaixo para iniciar o consumidor e começar a receber mensagens:

```bash
python consumer.py
```

## 🤝 Contribuição

Sinta-se à vontade para contribuir! Fique à vontade para abrir issues e pull requests.

## 📞 Contato

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/joschonarth/)
[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:joschonarth@gmail.com)
