
Neste módulo, usaremos a tabela `Produtos` que criamos. 

- Ela vai ter os campos:
	- ID
	- Nome
	- Cor
	- Preco
	- Tamanho 
	- Genero 
#### Built-in functions

**Built-in functions** são funções pré-existentes que auxiliam na manipulação de dados, como por exemplo contar, somar, média, etc. 

#### Usando o `COUNT`

```SQL
SELECT * FROM Produtos
```
Se fizermos isso, ele vai pegar todas as linhas da tabela. Se precisássemos contar quantas linhas a tabela tem, seria natural pensar que era só dar o SELECT e depois rolar lá pra baixo.

Mas, quando os bancos de dados começam a ficar grandes demais, fica inviável esperar carregar tudo sempre. Por isso usamos o `COUNT()`

- Prática
	```SQL
	SELECT COUNT(*) FROM Produtos
	```
	Aqui vai retornar a quantidade de linhas que tem, desse jeito:
	
	![[Pasted image 20240915164542.png]]
	
	Se quisermos dar nome para coluna que retorna o valor, fazemos assim:
	
	```SQL
	SELECT COUNT(*) QuantidadeProdutos FROM Produtos
	```
	
	![[Pasted image 20240915165230.png]]

- Busca mais detalhada
	```SQL
	SELECT COUNT(*) QuantidadeProdutosTamanhoM FROM Produtos WHERE Tamanho = 'M'
	```

---
#### Usando o `SUM`

Na tabela, temos uma coluna chamada `preco`, e imagine que queremos fazer uma soma do preço total dos meus produtos.

```SQL
SELECT SUM(Preco) PrecoTotal FROM Produtos
```
Neste caso, retornou *1784,70*

E assim como o COUNT, podemos colocar um WHERE
```SQL
SELECT SUM(Preco) PrecoTotal FROM Produtos WHERE Tamanho = 'M'
```
Neste caso, retorna *543,41*

---
#### Usando o `MIN`, `MAX` e `AVG`

```SQL
SELECT MAX(Preco) MaiorPreco FROM Produtos
```

```SQL
SELECT MIN(Preco) MenorPreco FROM Produtos
```

```SQL 
SELECT AVG(Preco) MediaPreco FROM Produtos
```

Todos conseguem usar o WHERE tb

---
#### Concatenando colunas

```SQL
SELECT  
	Nome + ' - ' + Cor
FROM Produtos
```

Retorna uma lista de coisas como:
	*"Mountain Bike Socks, M - Branco"*

---
#### `UPPER` e `LOWER`

```SQL
SELECT UPPER(Nome) FROM Produtos
```

```SQL
SELECT LOWER(Nome) FROM Produtos
```

---
#### Adicionando uma nova coluna

- De modo visual:
	![[Pasted image 20240915171244.png]]'

- Pelo Script
	Alterando a Tabela, e adicionando `DataCadastro` e seu tipo
	```SQL
	ALTER TABLE Produtos
	ADD DataCadastro DATETIME2
	```
	Mas, se não colocarmos dados, vai ficar tudo preenchido como `NULL`
	
	```SQL
	ALTER TABLE Produtos
	ADD DataCadastro DATETIME2
	
	UPDATE produtos SET DataCadastro = GETDATE()
	```
	Estamos fazendo um UPDATE sem WHERE, mas porque queremos atualizar todos, sem exceção.

Para apagar a coluna, faríamos assim:
```SQL
ALTER TABLE Produtos
DROP COLUMN DataCadastro
```

---
#### Formatando uma data

```SQL
SELECT
	FORMAT(DataCadastro, 'dd-MM-yyyy hh:mm') Data
FROM Produtos
```

Se quisermos que a hora seja em formato de 24h colocamos o `HH` em maiúsculo

---
#### Entendendo o `GROUP BY`

Se quisermos contar a quantidade que temos de cada produto por tamanho. Ex:
- M - 4
- G - 19
- etc

Vamos fazer assim:
```SQL
	SELECT 
		Tamanho,
		COUNT(*) Quantidade
	FROM Produtos
	GROUP BY Tamanho
```

Para tratarmos valores nulo (fazer com que não apareçam)
```SQL
	SELECT 
		Tamanho,
		COUNT(*) Quantidade
	FROM Produtos
	WHERE Tamanho <> '' -- Aonde tamanho seja diferente de vazio
	GROUP BY Tamanho
	ORDER BY Quantidade DESC
```

- `<>` 
	- Diferente. Também funciona `!=`

---
#### Primary Key e Foreign Key

- **Primary Key (PK):** Chave única que identifica cada registro na tabela
- **Foreign Key (FK):** Chave que identifica um registro existente em outra tabela

Criando uma tabela de Endereços com uma FOREIGN KEY
```SQL
SELECT * FROM Clientes

CREATE TABLE Endereços {
	Id int PRIMARY KEY INDETITY(1,1) NOT NULL,
	IdCliente int NULL,
	Rua varchar(255) NULL,
	Bairro varchar(255) NULL,
	Cidade varchar(255) NULL,
	Estado char(2) NULL,
	
	CONSTRAINT FK_Enderecos_Clientes FOREIGN KEY(IdCliente)
	REFERENCIES Clientes(Id)
}
```

- `CONSTRAINT FK_Enderecos_Clientes`
    - `CONSTRAINT`: Indica que estamos definindo uma restrição.
    - `FK_Enderecos_Clientes`: É o nome dado a essa restrição específica. Geralmente, "FK" significa "Foreign Key" (Chave Estrangeira) e o restante do nome indica as tabelas envolvidas na relação.
    
- `FOREIGN KEY(IdCliente)`
    - `FOREIGN KEY`: Especifica que o campo "`IdCliente`" é uma chave estrangeira.
    - `(IdCliente)`: Indica o nome do campo na tabela atual que contém a chave estrangeira.
    
- `REFERENCES Clientes(Id)`
    - `REFERENCES`: Estabelece a relação com a tabela de referência.
    - `Clientes(Id)`: Indica que a chave estrangeira "`IdCliente`" se refere à chave primária "Id" da tabela "Clientes".
    
- **Significado:**
	
	Essa restrição significa que o campo "`IdCliente`" na tabela onde essa restrição está sendo definida (provavelmente uma tabela chamada "`Enderecos`") deve conter apenas valores que existam no campo "`Id`" da tabela "`Clientes`". Em outras palavras, cada endereço (registro na tabela "`Enderecos`") deve estar associado a um cliente existente (registro na tabela "`Clientes`").

Continuação:
```SQL
SELECT * FROM Enderecos
INSERT INTO VALUES (4, 'Rua teste', 'Bairro teste', 'Cidade teste', 'SP')
-- Id (cria automáticamente), IdCliente, Rua, Bairro, Cidade, Estado
```

---
#### Realizando um JOIN
*INNER JOIN*

```SQL
SELECT 
	*
FROM
	Clientes 
INNER JOIN Enderecos ON Clientes.Id = Enderecos.IdCliente
WHERE Clientes.Id = 4
```
Ele vai juntar as tabelas

```SQL
SELECT 
	*
FROM
	Clientes -- seleciona a tabela clientes
INNER JOIN Enderecos -- junta com a tabela endereços
ON Clientes.Id = Enderecos.IdCliente -- Aonde Cliente.Id é igual Enderecos.Cliente
WHERE Clientes.Id = 4 -- E mostra só o que tem Clientes.Id = 4
```

Vai aparecer os dados das colunas Clientes e Endereços juntos, como se continuassem um ao outro.

Se fizermos o `JOIN`, dá pra pegar os dados das duas tabelas em um único `SELECT`
```SQL
SELECT
	Clientes.Nome,
	Clientes.Sobrenome,
	Clientes.Email,
	Enderecos.Rua,
	Enderecos.Bairro,
	Enderecos.Cidade,
	Enderecos.Estado
FROM
	Clientes
INNER JOIN Enderecos ON Clientes.Id = Enderecos.IdClientes
WHERE Clientes.Id = 4
```

tb dá pra fazer assim:
```SQL
SELECT
	C.Nome,
	C.Sobrenome,
	C.Email,
	E.Rua,
	E.Bairro,
	E.Cidade,
	E.Estado
FROM
	Clientes C
INNER JOIN Enderecos E ON C.Id = E.IdClientes
WHERE Clientes.Id = 4
```
Estamos criando um ***Alias*** aqui

### Tipos de `JOIN`
![[Pasted image 20240919200532.png]]