___
#### Objetivo Geral

Aprender os principais conceitos de banco de dados, SQL, comandos, tratamento e junção de dados, com foco em desenvolvimento.

---
### Banco de dados

##### Introdução
Um banco de dados é uma coleção organizada de informações (ou dados) estruturadas, normalmente armazenadas eletronicamente em um sistema de computador.

![[Pasted image 20240911142701.png]]

- temos alguns sistemas que acessam o banco de dados, entre eles:
	- API's
	- Sistemas em Nuvem
	- Cliente que acessa Sistemas Web que acessa o nosso banco

O banco de dados seria o nosso repositório de dados. Ele vai ser por exemplo, instalado em um servidor, e o software do banco disponibilizaria para quem tem acesso. Somente pessoas e sistemas autorizados podem acessa-lo.

Ele não só guarda dados, ele guarda da melhor maneira e atende as requisições de forma inteligente.

##### Tipos de bancos de dados
*Temos dois principais tipos que são mais utilizados:*

###### **Banco de dados relacional:** 
O tipo mais usado atualmente, armazenando dados estruturados, sendo organizado em tabelas, com colunas e linhas, que se relacionam entre si.

- Exemplos:
	- Microsoft SQL Server
	- Oracle Database
	- MySQL <-- gratuito


- **Entendendo uma tabela**
	
	- **Tabela:** São dados estruturados e organizados logicamente em formate de linha e coluna.
	
	![[Pasted image 20240911145836.png]]
	- *o ID representa o índice das linhas*
	
	- Nos poderíamos colocar todos os dados na tabela de clientes, mas o ideal, é separarmos as tabelas baseando-se nos contextos. 
	
	 - As tabelas se relacionam, e para isso, elas precisam apontar para outra tabela, neste caso, a tabela *"`Endereços`"*  tem a chave `IdCliente` para apontar para a tabela `Clientes`
	 
	- A primeira linha da tabela de endereços, nesse caso, aponta pra primeira linha da tabela de Clientes com o `IdCliente 1`, então Leonardo Buta mora na Rua 1.

###### **Banco de dados não relacional**

Banco de dado onde os dados não são armazenados em tabela, mas sim armazenados de maneira não estruturadas ou semi-estruturadas.

- Exemplo: MongoDB

Existem vários tipos: document databases, key-value databases, wide-column stores, e graph databases.

Ele é bastante usado em conceitos de Big Data, Mobile, Flexibilidade de Dados. Por ser mais rápido justamente por não ter tantas regras. O ruim é que não dá pra relacionar esses dados, até dá, mas é bem ruim.

---
#### Tipos de dados

![[Pasted image 20240911151951.png]]

Principais diferenças:
- estruturado:
	- Temos as colunas e as linhas, se quisermos remover uma coluna, ela será removida para todos, não dá pra remover pra um tipo só. Como, remover a coluna `Email` só para a coluna `Nome`.
	- Se quisermos colocar um datetime na coluna `Email` não vai dar, porque só aceita texto, o banco de dados estruturado tem essas regras mais rígidas.
- semi-estruturado
	- De certa forma, ele tem um padrão, nesse caso chave-valor
	- Mas nem todos seguem o mesmo formato, nesse caso o Id2 tem um novo campo, chamado `Cupom` e o valor do Preço tem tipos diferentes entre os Id's

---
#### Entendendo o DBMS

**Database Management System:** É um software utilizado para acessar, manipular e monitorar um sistema de banco de dados.

![[Pasted image 20240911161423.png]]

Por si só, o banco de dados funciona sozinho. Mas você tb tem o DBMS que é basicamente, a interface gráfica interativa do banco de dados, onde interagimos com o banco. Nesse caso, o do SQL Server, se chama ***SQL Server Management Studio***.

