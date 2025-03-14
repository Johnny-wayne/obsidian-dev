O Express.js é um framework minimalista e flexível para Node.js que facilita a criação de aplicações web e APIs. 

Ele oferece uma camada fina de funcionalidades essenciais, como ***roteamento***, ***middleware*** e ***templates***, sem comprometer a flexibilidade do Node.js. Em outras palavras, o Express.js é como um esqueleto que você personaliza para construir sua aplicação.

1. **Instalação:**
	
	```Bash
	npm init -y
	npm install express
	```
	
	O comando `npm init -y` cria um arquivo `package.json` para gerenciar as dependências do seu projeto. O comando `npm install express` instala o módulo Express.js.

2. **Criando um arquivo JavaScript:**
	
	```JavaScript
	const express = require('express');
	const app = express();
	const port = 3000;
	
	app.get('/', (req, res) => {
		res.send('Hello, World!');
	});
	
	app.listen(port, () => {
		console.log(`Servidor rodando na porta ${port}`); 
	});
	```

3. **Explicando o código:**
    
    - `require('express')`: Importa o módulo Express.js.
    
    - `const app = express()`: Cria uma instância do aplicativo Express.
    
    - `app.get('/', (req, res) => { ... })`: Define uma rota GET para a raiz (`/`). Quando alguém acessar o seu servidor na raiz, a função dentro do `app.get` será executada.
    
    - `res.send('Hello, World!')`: Envia a resposta para o cliente, neste caso, a string "Hello, World!".
	
    - `app.listen(port, () => { ... })`: Inicia o servidor na porta especificada (3000).