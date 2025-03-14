
### Start
#### A linguagem SQL

***SQL (Structured Query Language):*** É a linguagem de banco de dados usada para consulta e manipulação de dados. Quase todos os bancos de dados estruturados usam a linguagem SQL.

![[Pasted image 20240911195451.png]]

DCL e TCL não veremos por enquanto

TCL = volta que deu merda

---
#### Entendendo um database

**Database:** É uma coleção de dados estruturados, agrupados de forma concisa. É composto de tabelas, procedures, views, etc.

![[Pasted image 20240911214740.png]]

Dá pra agrupar databases de vários sistemas em um único servidor database (nesse exemplo é local).

---
#### Acessando o banco de dados

- **Configurações iniciais:** 
	- Normalmente o banco de dados abre junto com o PC automaticamente, mas não queremos isso, porque come memória e processamento, mesmo que pouca, é ruim.
	- Então vamos pesquisar  *`SQL configuration manager`* e abrir ele.
	- Depois vamos em *`SQL Server Services`* dentro do programa que abrimos.
	- Vamos no *`SQL Server`* que está rodando e vamos em suas *`propriedades`* depois `services` e procuro por *`modo inicial`* lá dentro, e coloque para ***"manual"***.
	
	- Agora, quando formos usa-lo, precisaremos inicia-lo manualmente e para-lo manualmente. Clicando com o botão direito nele.

- **Logando no SQL Studio**
	- As configurações iniciais para logar no SQL Server, vão ser essas: 
		![[Pasted image 20240912114719.png]]
		- **Server Type:** O tipo de servidor, nesse caso, vamos usar *Database Engine*
		- **Server name:** Esse *server name* é relacionado aquela string lá que deram na instalação
		- **Authentication:** Ele reconhece o usuário do Windows e permite o login
			- Caso formos usar um banco de dados remoto ou externo, precisaremos mudar o tipo de autenticação para *SQL server authentication* e colocar login e senha.

- **Entendo o primeiro contato:**
	
	- Inicialmente, o banco de dados, vem sem nenhum database além dos defaults, esse daí `ExemploDB`, criei agora, clicando com o botão direito em cima da pasta `Databases`. Só precisa botar um nome.
		![[Pasted image 20240912115807.png]]
	- Aí se quisermos fazer a famosa **Consulta**, vamos ter que vir aqui em **`New Query`**
		![[Pasted image 20240912120141.png]]
	- Sempre que formos criar uma query, precisamos nos atentar se está apontando para o DB que queremos:
		![[Pasted image 20240912120502.png]]
		- Neste caso, está apontando para o DB que queremos, mas às vezes aponta par ao ***`Main`*** que é o DB do sistema, não mexemos nele

---
#### Tabelas

Inicialmente, criamos o DB `ExemploDB` e baixamos e executamos um arquivo de script SQL para criação de uma tabela com alguns dados. 
	*Ele tava com bug, provavelmente porque o meu SQL é diferente do que o instrutor possui. O bug estava no formato de Data e hora, pedi para o Gemini studio analisar e corrigir*

![[Pasted image 20240912153453.png]]

Aí naquela nova Query do `ExemploDB` que abrimos, colocamos:
```SQL
SELECT * FROM Clientes
```

Já vimos isso, ele seleciona os dados de todas as colunas da tabela Clientes. E mostra uma ***"Result Grid"*** ou simplesmente uma *grid de resultados*.

---
### Mid

#### Querys

##### Ordenando resultados

Se quisermos ordenar os resultados, usamos o `ORDER BY`
```SQL
SELECT * FROM Clientes
ORDER BY Nome
```
Nesse caso, ele colocaria em ordem alfabética os nomes

```SQL
SELECT * FROM Clientes
ORDER BY Nome DESC 
```
Mesma coisa só que em ordem decrescente, crescente é `ASC`, mas é desnecessário, porque o `ORDER BY` sempre considera primeiro de forma crescente.

```SQL
SELECT * FROM Clientes
ORDER BY Nome, Sobrenome
```
Ordena primeiro por `Nome` e depois por `Sobrenome`

---
##### Selecionando colunas

Por enquanto estamos trabalhando com `*` para selecionar todas as colunas mas se quisermos trabalhar com colunas específicas, usamos:

```SQL
SELECT Nome, Sobrenome, Email FROM Clientes
ORDER BY Nome, Sobrenome
```
É boa prática trazer apenas colunas que você precisa.

---
##### Utilizando o `WHERE`

Ela é utilizada quando queremos determinar certos tipos de dados. Quando queremos pegar algo mais específico. Por exemplo:

```SQL
SELECT * FROM Clientes
WHERE Nome = 'Adam'
ORDER BY Nome, Sobrenome
```
A consulta retornará apenas clientes com Nome = Adam.

Se quisermos ser mais específicos ainda:
```SQL
SELECT * FROM Clientes
WHERE Nome = 'Adam' AND Sobrenome = 'Reynolds'
ORDER BY Nome, Sobrenome
```
Também temos o `OR`, já sabemos o que ele faz.

---
##### Utilizando o `LIKE` 

É uma Query um pouco mais específica.
Por exemplo, eu quero filtrar todos os meus clientes que comecem com G.

Aqui dá erro, porque ele procura clientes que tenham o Nome ***G*** com o `WHERE`
```SQL
SELECT * FROM Clientes
WHERE Nome = 'G'
ORDER BY Nome, Sobrenome
```

É assim que a gente faz
```SQL
SELECT * FROM Clientes
WHERE Nome LIKE 'G%'
ORDER BY Nome, Sobrenome
```

O `LIKE` serve para fazermos uma consulta de caractere único.
Nesse caso `G%` significa: *"Tem que ter G no começo e o que estiver em diante, pouco me importa."*

Também podemos fazer assim:
```SQL
SELECT * FROM Clientes
WHERE Nome LIKE '%G%'
ORDER BY Nome, Sobrenome
```
Neste caso, estamos trazendo todos que têm a letra  ***G*** no nome.

---
##### Realizando um `INSERT`

###### Não omitindo as colunas

```SQL
INSERT INTO Clientes (Nome, Sobrenome, Email, AceitaComunicados, DataCadastro)
VALUES ('Leonardo', 'Buta', 'email@email.com', 1, GETDATE())
```

- `GETDATE()` 
	- Pega a data e hora atual, vai ser explicado melhor mais pra frente

-  Como funciona uma Query
	É um arquivo de texto comum e podemos ter vários comandos dentro dele, como o que estamos vendo. Se colocarmos 2 comando `SELECT` ele irá realizar duas consultas para nós, irá nos mostrar duas tabelas.
	
	Se selecionarmos a clausula, ou parte da Query, que queremos executar (com o mouse mesmo), e executarmos, ele executará apenas aquela parte. Se não selecionarmos, ele seleciona tudo.

Aí para vermos se conseguimos adicionar esse dado, fazemos uma consulta:

```SQL
INSERT INTO Clientes (Nome, Sobrenome, Email, AceitaComunicados, DataCadastro)
VALUES ('Leonardo', 'Buta', 'email@email.com', 1, GETDATE())

SELECT * FROM Clientes WHERE Nome = 'Leonardo'
```

###### `INSERT` omitindo as colunas

```SQL
-- Não omitindo as colunas
--INSERT INTO Clientes (Nome, Sobrenome, Email, AceitaComunicados, DataCadastro)
--VALUES ('Leonardo', 'Buta', 'email@email.com', 1, GETDATE())

--Omitindo as colunas
INSERT INTO Clientes VALUES ('Leonardo', 'Buta', 'email@email.com', 1, GETDATE())


SELECT * FROM Clientes WHERE Nome = 'Leonardo'
```

- Diferença:
	- Omitindo as colunas temos uma sintaxe menor
	- Não omitindo, podemos mudar a ordem que colocamos os valores.

###### Entendendo ID

Ele é o identificador único da coluna, também conhecido como ***Primary Key***.
Ele basicamente diz que aquela linha é única. É o que diferencia as linhas que às vezes possuem valores iguais.

Mesmo deletando, ele continuar a contagem. Por exemplo, se criarmos a linha id 1 e 2 e apagarmos a 2, quando criarmos outra, ele irá criar a linha 3 e não a 2 de novo.

Se perceber, não passamos o ID na hora que criamos as linhas anteriormente. Isso acontece, porque não é necessário passarmos, o próprio banco já cria e implementa para nós. 

*Obs: a coluna Id, poderia ter qualquer outro nome.*

---
##### Cuidados quando se conectar

Quando abrimos uma Query, ela está apontando para uma determinada Database. Quando conectamos nosso banco de dados, por padrão, ele se conecta no Database ***Master***, que é o Database do sistema que não vamos trabalhar.

---
##### Realizando um Update

Serve para alterar dados.

Se fizermos assim, ele vai mudar TODOS os campos de Email
```SQL
SELECT * FROM Clientes WHERE Nome = 'Eduardo'

UPDATE Clientes
SET Email = 'emailatualizado@gmail.com'
```

Se fizermos assim, aí ele só vai atualizar o valor Email da linha com o Id 1003 que neste caso, é do 'Eduardo'
```SQL
SELECT * FROM Clientes WHERE Nome = 'Eduardo'

UPDATE Clientes
SET Email = 'emailatualizado@gmail.com'
WHERE Id = 1003
```

Se quisermos atualizar mais valores, fazemos assim:
```SQL
SELECT * FROM Clientes WHERE Nome = 'Eduardo'

UPDATE Clientes
SET Email = 'emailatualizado@gmail.com',
	AceitaComunicados = 0
WHERE Id = 1003
```

###### Cuidados com o Update

Depois que fizermos o `UPDATE`, **já era paizão**.

```SQL
SELECT * FROM Clientes WHERE Nome = 'Eduardo'

BEGIN TRAN -- Quando colocamos BEGIN TRAN estamos trabalhando em um modo que dá pra voltar, caso dê ruim
ROLLBACK 

UPDATE Clientes
SET Email = 'emailatualizado@gmail.com',
	AceitaComunicados = 0
```

Aí, aqui, quando der bosta e ter atualizado tudo para todo mundo, só rode a clausula `ROLLBACK`,  que volta tudo ao normal

---
##### Deletando um registro

```SQL
SELECT * FROM Clientes WHERE Nome = 'Leonardo'

DELETE Clientes
WHERE Id = 1001
```
Acho que é bem autoexplicativo. 

Assim como o `UPDATE` se não tiver `WHERE` fodeo. Então por garantia, usa o BEGIN TRAN ROLLBACK 

---
#### Estudando os tipos de dados

Criação de tabelas:
```SQL
-- Criação da tabela
CREATE TABLE Clienets
	Id int IDENTITY(1,1) NOT NULL,
	Nome varchar(255) NULL
	Sobrenome varchar(255) NULL,
	Email varchar(255) NULL,
	AceitaComunicados bit NULL,
	DataCadastro datetime2(7) NULL
```

###### Tabelas com os tipos de dados:

- String Data Types
	![[Captura de tela 2024-09-15 133129.png]]
	Os tipos que mais usaremos, serão os tipos: 
	- `char(n)` quantidade fixa de caracteres
	- `varchar(n)` quantidade variável de caracteres
	
- Numeric Data Types
	![[Captura de tela 2024-09-15 133036.png]]
	![[Captura de tela 2024-09-15 133047.png]]
	Aqui não tem muito pra onde fugir, a gente usa bastante a maioria deles.	
	
- Date and Time Data Types
	![[Captura de tela 2024-09-15 133054.png]]
	Vamos usar na maioria dos casos, apenas o `datetime2`

---
#### Criando uma tabela

```SQL
CREATE TABLE Produtos {
	Id int IDENTITY(1,1) NOT NULL, -- significa que é obrigatório preencher
	Nome varchar(255) NOT NULL,
	Cor varchar(50) NULL, -- Pode ser nulo
	Preco decimal(13, 2) NOT NULL,
	Tamanho varchar(5) NULL,
	Genero char(1) NULL
}
```

É importante lembrar de adicionar isso:
```SQL
CREATE TABLE Produtos {
	Id int IDENTITY(1,1) PRIMARY KEY NOT NULL, -- aqui
	Nome varchar(255) NOT NULL,
	Cor varchar(50) NULL, 
	Preco decimal(13, 2) NOT NULL,
	Tamanho varchar(5) NULL,
	Genero char(1) NULL
}
```

- `PRIMARY KEY`
	- Isso torna o ID algo único, que não pode se repetir

Podemos manipular dados de uma tabela, como inserir, atualizar e remover dados. Esses comandos juntos são conhecidos como:  
DML (Data Manipulation Language)

Existe um comando no DDL (Data Definition Language) usado para criar uma tabela. Esse comando é conhecido como:

Existe um comando no DQL (Data Query Language) usado para obter dados de uma tabela. Esse comando é conhecido como:


