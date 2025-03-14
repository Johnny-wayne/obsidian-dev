*Structured Query Language*

--- 
>*É a terceira linguagem de programação mais popular sendo utilizada por 50% dos desenvolvedores e em abril de 2022, existiam mais de 53 mil vagas no Brasil para SQL abertas no LinkedIn. A segunda mais popular é **Python** e só possuía 33 mil vagas*

----
# CURSO SQL - Conquer Plus

--- 
## Módulo 1 - básico

---
### Softwares de SQL:

- SQLite
- Microsoft SQL Server
- MySQL
- Postgre SQL
- Google Big Query
- SAP Hana Studio

---- 
### Estrutura de Informações

É uma estrutura de informações com:
- Colunas ou campos
- Linhas ou informações
Cada linha vai ter uma informação de um campo diferente
Planilha = tabela

Campo exemplo:
- Idade
- Nome
- Endereço

Informações exemplo:
- 23
- Bia
- Campinas

----
#### Estamos usando [[SQLite]] Online e temos 3 tabelas:
- Product
- Sales
- Customers

---
### Primeiras Querys

- SELECT - O que você quer visualizar
- FROM  -  Da onde você quer visualizar

> [!info] Contexto:
>Você trabalha em uma empresa e pra já sair na frente eles te pedem pra pegar os dados dos **produtos** mais caros

Use o * entre o SELECT e o FROM para trazer todos os campos da tabela.
Caso não saiba os campos que quer selecionar faça isso pra dar uma espiada.

O [[SQL Conquer]] não tem necessidade de endentação como o **Python** por exemplo. Só é recomendado deixar organizado para saber melhor onde as coisas estão.

```SQLite
SELECT product_name, price FROM Product;
```

O ; é usado pra separar blocos de código, no [[SQLite]] não é tão usado

```SQLite
SELECT product_name, price FROM Product ORDER BY price DESC
```

O padrão do SQL é de apresentação em valores crescente, então foi apresentado dos menores preços, aos maiores. Por isso colocamos `DESC`, para colocar de forma decrescente
De resto, acho que já tá bem alto explicativo

Para limitar para apenas os 5 primeiros produtos é só colocar a query `LIMIT` no final do código

```SQLite
SELECT product_name, price FROM Product ORDER BY price Desc LIMIT 5
```

O LIMIT não vai funcionar em todos os bancos de dados, caso não funcione no banco de dados da minha empresa. É só mudar para TOP, ele sempre vai vir depois do SELECT.

Exemplo:
`SELECT TOP 5`

-----
### Selecionando informações específicas
*Usando WHERE*

> [!info] Contexto:
> Dentro da categoria "Tecnologia", quais são os 15 produtos:
>- mais baratos;
>- com o valor acima de R$10;
>- Ou que seja acessório?

Para isso vamos usar o WHERE, ele é um limitador, diz onde eles estão.
No WHERE existem várias chaves:

| =        | igual                                                                             |
| -------- | --------------------------------------------------------------------------------- |
| != ou <> | diferente                                                                         |
| <=       | menor igual                                                                       |
| >=       | maior igual                                                                       |
| >        | maior                                                                             |
| <        | menor                                                                             |
| BETWEEN  | intervalo de dados/texto                                                          |
| IN       | se você precisa criar uma lista dentro do seu WHERE para ele procurar nessa lista |
| NOT IN   | se você quer que ele busque o que NÃO tem na sua lista                            |
| LIKE     | se quer fazer uma busca aproximada                                                |

Se está procurando texto você precisa usar as aspas simples pra saber que é texto
```Sql
SELECT * FROM Product WHERE category = "Technology"
```


> [!tip] Nem sempre as tabelas estarão com letras todas maiúsculas ou minúsculas
> Utilize UPPER ou LOWER para padroniza-las na busca de textos
> 
> ```SQL
 SELECT * FROM Product WHERE lower(category) = "technology"
> ```


> [!Failure] Aspas simples 'Text'
> A moça disse pra usar aspas simples 'Text', mas deu erro e só funcionou com aspas normais "Text"

OR e AND
```sql
SELECT * FROM Product 
WHERE lower(category) = "technology"
AND ( price > 10 OR lower(sub_category) = "acessories" )

Order BY price
LIMIT 15
```
Precisa colocar o AND dentro dos parênteses para encapsular o OR e manter o technology


> [!todo] DESAFIO
> - 10 produtos mais caros
> - Fora da categoria tecnologia 
> - com o valor máximo de R$1.000

***Resultado:***

```sql
SELECT * FROM Product 
WHERE 
	lower(category) != ("technology") /* Dá pra colocar NOT IN no lugar do != */
 AND ( price <= 1000 )
 
 Order BY price DESC
 Limit 10
```
Aqui precisou colocar o technology dentro dos parênteses porque não tava reconhecendo como coluna, mas como tabela

--- 

## Módulo 2 - Intermediário

---
### Trabalhando com agregações: COUNT, SUM, MAX, MIN, AVG

> A inabilidade de conectados dados a valor de negócio é o ***Segundo maior impedimento*** para o sucesso de um time que trabalha com dados

**\- Gartner, 2020.**

 ***Contexto***

- Quantos produtos a ***Conquer Sales*** tem no catálogo?
	-  Qual a média dos preços?
	-  Qual é o maior e o menor valor deles?

Para isso vamos usar as funções de agregação

| | |
|---|-|
| COUNT | Vai contar a quantidade de linhas em uma tabela, caso use o DISTINCT, ele vai mostrar a quantidade distinta de uma coluna na tabela
| AVG | Vai dar a média de valores que tem uma tabela |
| MAX | Vai pegar o meu maior valor |
| MIN | Vai pegar o meu menor valor |


```sql
SELECT
COUNT(*) ,
	COUNT(product_id)
FROM Product 
```

>[!warning] Cuidado!
> Aqui ele vai passar o valor da quantidade de linhas que `product_id` possui. Caso ele se repita na tabela, também será contabilizado no valor final.
> Por isso use `DISTINCT` antes do `product_id`. Para pegar sem repetições. 
```sql
SELECT
	COUNT(*) ,                  /* Essa é só uma contagem geral, não aparece*/
	COUNT(DISTINCT product_id) /* O resultado de produtos é exibido nessa linha*/
FROM Product 
```

Aparece um bagulho assim:

|  `Count(*)`   |  `Count(product_id)`  |
|---|---|
|1893 | 1893|

Mas se quiser deixar mais apresentável e bonitinho:
```sql
SELECT
	COUNT(*) AS TOTAL_LINHAS,     
	COUNT(DISTINCT product_id) AS TOTAL_PRODUTOS
FROM Product AS P
```

Aparece um bagulho assim:

|  TOTAL_LINHAS   | TOTAL_PRODUTOS  |
|---|---|
|1893 | 1861|

Agora já sabemos o total de produtos, precisamos agora saber a média dos preços e o menor e maior valor deles. Para isso:

```sql
SELECT
	COUNT(*) AS TOTAL_LINHAS  
  , COUNT(DISTINCT product_id) AS TOTAL_PRODUTOS
  ,	AVG(price) AS MEDIA_VALOR
  , MAX(price) AS MAIOR_VALOR
  , MIN(price) AS MENOR_VALOR
FROM Product AS P
```

Aparece um bagulho assim:

|  TOTAL_LINHAS   | TOTAL_PRODUTOS  | MEDIA_VALOR | MAIOR_VALOR | MENOR_VALOR |
|-----------------|-----------------|-------------| ------------|-------------|
|1893 | 1861 | 141.4288748019016| 22638.48 | 0.44 |
Na próxima a gente vai fazer isso por categorias.

--- 
### Trabalhando com agregações GROUP BY e DISTINCT

```sql
SELECT category
FROM product
GROUP BY category
```

Aparece isso:

| Category | |
|-----------|- |
|Furniture | |
|Office Supplies| |
| Technology | |

Outra forma de fazer isso é:
```sql
SELECT DISTINCT category
FROM product
```

As vantagens de um ou de outro vão ser na parte do processamento do banco e vão depender de banco para banco.

```sql
SELECT 
  category
  ,	COUNT(*) AS TOTAL_LINHAS  
  , COUNT(DISTINCT product_id) AS TOTAL_PRODUTOS
  ,	AVG(price) AS MEDIA_VALOR
  , MAX(price) AS MAIOR_VALOR
  , MIN(price) AS MENOR_VALOR
FROM Product AS P
GROUP BY category
```

Aparece um bagulho assim:

| Category |  TOTAL_LINHAS   | TOTAL_PRODUTOS  | MEDIA_VALOR | MAIOR_VALOR | MENOR_VALOR |
| -------- |-----------------|-----------------|-------------| ------------|-------------|
| Furniture | 383 | 375 | 145.271 | 1497.64 | 1.49 |
| Office Supplies |1097 | 1082 | 50.820| 3930.07 | 0.44 |
| Technology |413 | 404 | 378.537| 22638.48.48 | 0.99 |

#### Ordem das Querys:
*Sempre vai ser nessa ordem:*

- SELECT  ----> Colunas que quero e que aparecem
- FROM  -----> Da onde elas vem
- WHERE -----> Filtro
- GROUP BY ---> Divide as tabelas por:
- ORDER BY ---> Ordena as linhas por:
- LIMIT

Desses só o LIMIT não funciona em todos os SQL´s

***Contexto:***

- Qual é o top 8 de subcategorias, filtrando valores **maiores do que R$ 10 e menores do que R$ 1000?**
- Ordene pelo valor médio de preço e, além da subcategoria, traga também a categoria, o valor total dos produtos e a média de preço deles.

```sql
SELECT
	sub_category
  , category
  ,	SUM(price) valor_total
  , AVG(price) valor_medio
FROM Product
WHERE prices BETWEEN 10 AND 1000
GROUP BY 
	sub_category
	, category
ORDER BY valor_medio
LIMIT 8;

```
Aqui `valor_medio` é a ***quarta*** coluna, é o índice dela, então dá pra fazer assim também:

```sql
ORDER BY 4
```

> [!tip] Bases muito grandes ou em nuvem
> Caso a base de dados do trampo for muito grande ou for em nuvem, use sempre o `LIMIT` ele vai deixar bem mais otimizado e vai ter uma resposta mais rápida.


---
### Enriquecendo sua base: LEFT JOIN

***Contexto***
- Dos produtos que estão no top 5, quantas vendas foram feitas de cada produto?

```SQL
SELECT 
	P.product_name
    , P.price
    , COUNT(DISTINCT S.order_id) QNT_VENDAS
FROM Product P 
LEFT JOIN Sales S 
	On S.product_id = P.product_id
GROUP By 
	P.product_name
	, P.price 
Order by price DESC
LIMIT 5
```
É...
O  bagulho ficou meio complicado agora né?

`LEFT JOIN`  serve para juntar a tabela = PROCV do Excel
O SQL vai buscar as informações pelo ***FROM*** e depois juntar a tabela com o ***LEFT JOIN***

> [!note] Se encontrar a informação vai ser preenchida, se não, vai retornar ***null*** ou vazio

***Contexto:***
A equipe de marketing quer selecionar as empresas que menos vendemos para impulsionar as vendas. Quais são as 10 cidades em que menos vendemos desde que começamos a empresa?

```SQl
SELECT

FROM Sales S
LEFT JOIN Customer C
	ON S.customer_id = C.customer_id
```

> [!tip]
> Primeiro selecione desse jeito, para depois ir preenchendo. Pegue primeiro da onde a informação vem

continuação:
```SQl
SELECT
	c.city
	, COUNT(DISTINCT S.order_id) qntd_vendas
FROM Sales S
LEFT JOIN Customer C
	ON S.customer_id = C.customer_id
GROUP BY C.city
ORDER BY 2
LIMIT 10
```

> [!note] Se tem `COUNT` tem que ter `GROUP BY`

---
### Quando tenho mais fontes de dados: outros tipos de JOIN

![[SQL.png]]

***INNER JOIN:*** Ele pega só o que as duas tabelas tem em comum (é o de cima central)
 
E o resto eu acho que dá pra adivinhar.

***Contexto:***
Quais são os clientes que realizaram compras em abril, mês da campanha de marketing?

```sql
SELECT
S.*
, CA.city
FROM Sales S
LEFT JOIN campaign ca
ON CA.Custommer_id = S.Customer_id
WHERE S.Order_Date LIKE '2022-04%' #Tem que ser em abril né, então tá aí
```

Ficou um bagulho assim:
![[Dados.png]]

> [!warning] Aparecem vendas de cidades que não estavam na campanha de marketing como `null`

#### ***Solução:***
Trocar 
```sql
LEFT JOIN campaing CA
```
por
```sql
INNER JOIN campaing CA
```

> [!tip] Quanto mais ***otimizada*** sua consulta, menos trabalho pro seu banco de dados. Se usar menos dados, a consulta fica mais rápida

***Desafio***
Quais são as 10 cidades com maior valor de venda?

***Quero mais:***

exemplos de banco de dados:
- ##### Google Cloud
- ##### Banco de dados SQL do Azure

----
## Módulo 3 - Indo além
---
> **70%** dos negócios no mundo estão coletando dados mais rapidamente do que conseguem utiliza-los.
> 
> Enquanto que apenas **21%** das empresas sabem tratar os dados adequadamente

 \ - Data Paradox, Dell Technologies, 2020
 
--- 
***Missão:***
Aprofundar o conhecimento de SQL, a partir de funções que permitem uma análise mais detalhada e otimizada de dados.

--- 
### Quando é preciso criar separações: CASE WHEN

***Exemplo de uso:***

```sql
CASE 
	WHEN condição1 THEN resultado1
	WHEN condição2 THEN resultado2
	ELSE resultado3
END
```
Vai até 10 linhas

***Contexto:***
Ainda sobre o catálogo da Conquer Sales, em quantas categorias diferentes há produtos na cor cinza?

```sql
SELECT
category
, product_name
, CASE When UPPER(product_name) LIKE "%GRAY%"
	THEN 'SIM'
	ELSE 'NAO'
  END AS VALIDADOR
FROM Product
``` 

Dá isso:
![[Dados 2.png]]
Deu um monte de `NAO` então obviamente está errado

- Então a gente faz isso aqui ó:
```sql
SELECT
category
, product_name
, CASE When UPPER(product_name) LIKE "%GRAY%"
	THEN 'SIM'
	ELSE 'NAO'
  END AS VALIDADOR
, COUNT(DISTINCT category) AS QNTD_VENDAS
FROM Product
GROUP BY CASE When UPPER(product_name) LIKE "%GRAY%"
	THEN 'SIM'
	ELSE 'NAO'
  END AS VALIDADOR
``` 
No `GROUP BY` não é possível colocar só o nome da coluna como no `ORDER BY`.

Deu:

| Validador | QNTD_VENDAS |
|------------|------------------|
| NAO | 3 |
| SIM | 3 |

***Descoberta:***
Não tem tantas categorias para falarem que tem 'pouco cinza' e em todas as categorias tem produtos cinzas.

---

***Contexto:***
- Se agrupar as categorias entre "Furniture", "Office Supplies" e "Outros", quantos produtos com a cor cinza na descrição terá no total?
```sql
SELECT
CASE
	WHEN UPPER(category) = 'OFFICE SUPPLIES' THEN category
	WHEN UPPER(category) = 'FURNITURE' THEN category
	ELSE 'Others'
	END tipo_categoria
, SUM(CASE WHEN UPPER(category) LIKE "%GRAY%"
	THEN 1
	ELSE 0 
  END) AS VALIDADOR
, COUNT(DISTINCT category) AS QNTD_VENDAS
FROM Product
GROUP BY CASE
	WHEN UPPER(category) = 'OFFICE SUPPLIES' THEN category
	WHEN UPPER(category) = 'FURNITURE' THEN category
	ELSE 'Others'
	END
```
![[Dados 3.png]]

----
### O WHERE não funciona: HAVING
*Em casos bem específicos*

***Contexto:***
- Quais são os estados que tivemos entre 30 e 100 vendas?

***WHERE:*** Serve para consultas que utilizam colunas originais
***HAVING:*** Serve para funções de agregação e `GROUP BY`

Usar o WHERE neste contexto não irá servir

```SQL
SELECT
C.State
, COUNT(DISTINCT S.Order_ID) QTDE
FROM sales S
LEFT JOIN customer C
	ON S.customer_id = C.customer_id
GROUP BY C.State
HAVING QTDE BETWEEN 30 AND 100
```

![[Dados 4.png]]

> [!TIP] 
> ***WHERE*** para quando se quer **filtrar primeiro e agrupar depois**
> ***HAVING*** para quando se quer **agrupar primeiro e filtrar depois**

---
### Otimização de consultas: SUBQUERY & TEMPORARY TABLE

> Dado ***Pré-filtrado*** = ganho em ***Performance***

***Contexto:***
- Quais são as 3 cidades com maior valor de venda em Tecnologia no estado da Califórnia?

```SQL
SELECT 
C.city
, COUNT(DISTINCT S.Order_ID) QTDE
FROM Sales S
INNER JOIN 
	(SELECT *
	FROM product
	WHERE category = "Technology"
	) P
	ON S.Product_ID = P.product_id
INNER JOIN
	(SELECT * 
	FROM customer
	WHERE state = "california"
	) C
	ON C.customer_id = S.customer_id
GROUP BY
c.city
```

![[Dados 5.png]]

```SQL
SELECT 
C.city
, COUNT(DISTINCT S.Order_ID) QTDE
FROM Sales S
INNER JOIN 
	(SELECT *
	FROM product
	WHERE category = "Technology"
	) P
	ON S.Product_ID = P.product_id
INNER JOIN
	(SELECT * 
	FROM customer
	WHERE state = "california"
	) C
	ON C.customer_id = S.customer_id
GROUP BY
c.city
ORDER BY 2 DESC
LIMIT 3
```
Esse é o valor com o ***SUBQUERY***

***TEMPORARY TABLE:***
```SQL
CREATE TEMPORARY TABLE p AS
	SELECT *
	FROM product
	WHERE category = "Technology"
;
CREATE TEMPORARY TABLE C AS 
	SELECT * 
	FROM customer
	WHERE state = "california"
;
```

Depois é só apagar que dá pra selecionar dessa forma:
```sql
SELECT 
C.city
, COUNT(DISTINCT S.Order_ID) QTDE
FROM Sales S
INNER JOIN P ON S.Product_ID = P.product_id
INNER JOIN C ON C.customer_id = S.customer_id
GROUP BY
c.city
ORDER BY 2 DESC
LIMIT 3
```

***Contexto
- Quais são os 10 produtos mais vendidos no estado da Califórnia?

```sql
SELECT 
P.category
, P.product_name
, COUNT(DISTINCT S.Order_ID) QTDE
FROM Sales S
INNER JOIN P ON S.Product_ID = P.product_id
INNER JOIN C 
	ON C.customer_id = S.customer_id
GROUP BY
P.category
, P.product_name
ORDER BY 2 DESC
LIMIT 10
```

![[Dados 6.png]]

> [!tip]
> Teste o **tempo de execução** com um `LIMIT` para escolher entre `SUBQUERY` e `TEMPORARY TABLE`

Na próxima a gente vai ver funções de data que vai nos ajudar a ver os dados em uma linha do tempo

--- 
### Análise de datas: DATE & SUBTR
*Dependendo do banco de dados que você usa, vai ter diferença na forma que você escreve*

#### 3 principais para data:

- ***CURRENT_DATE***
- ***DATE()***
- ***STRFTIME***

***CURRENT_DATE:***
- Retorna como resultado a data atual

***DATE():***
- Retorna como resultado uma data no formato AAAA-MM-DD

***STRFTIME:***
- Retorna como resultado a data formatada de acordo com as especificações


***Contexto:***
- Quantas vendas tivemos no mês passado e qual foi o valor total das vendas?

```SQL
SELECT
SUBSTR(order_date, 1, 7) RECORTE_DATA
FROM Sales
```

> [!NOTE] O `SUBSTR` pega um pedaço do seu texto
> `SUBSTR(NOME_DA_COLUNA, APARTIR_DE_QUAL_CARACTER no caso o primeiro, QUANTOS_CARACTERES)`
 
Aparece como: 

| RECORTE_DATA | |
|------------------|--|
| 2022-02 | |
| 2021-09 | |
| 2021-01 | |
| 2019-09 | |
etc

Isso funciona porque na coluna `Order_Date` é texto, então trabalhar com `SUBSTR`.

Se eu quisesse 'Ano/Mês' em vez de 'Mês/Dia' Iria ser assim:

```SQL
SELECT DISTINCT
SUBSTR(Order_Date, 6, 5) RECORTE_DATA
FROM Sales
```

| RECORTE_DATA | |
|------------------|-|
| 02-06 | |
| 09-10 | |
| 01-09 | |
| 09-07 | |

Isso funciona pra qualquer texto, o único ponto é, qual é o carácter inicial e qual o tamanho da string que vc quer.

***Segunda forma:***

```sql
SELECT DISTINCT
STRFTIME('%Y-%m', Order_Date) RECORTE_DATA
FROM Sales
```

A primeira parte de verde mostra o formato que queremos, que no caso, é Ano e Mês.

Aparece como: 

| RECORTE_DATA | |
|------------------|--|
| 2022-02 | |
| 2021-09 | |
| 2021-01 | |
| 2019-09 | |

***Terceira forma:***
```sql
SELECT DISTINCT
STRFTIME('%Y-%m', Order_Date) RECORTE_DATA
FROM Sales
WHERE 
	DATE(CURRENT_DATE , 'START OF MONTH' , '-1 MONTH')
#Puxa a data de hoje, primeiro dia do mês, um mês pra trás da data de hoje
```


> [!failure] Assim não dá
> Não dá pra comparar Texto com Data
```sql
SELECT DISTINCT
STRFTIME('%Y-%m', Order_Date) RECORTE_DATA
FROM Sales
WHERE 
	order date = DATE(CURRENT_DATE , 'START OF MONTH' , '-1 MONTH')
```


> [!failure] Assim não dá também
> Porque tá pedindo pra buscar um dia só
```sql
SELECT DISTINCT
STRFTIME('%Y-%m', Order_Date) RECORTE_DATA
, order_date #pra validar se tá buscando no lugar certo
FROM Sales
WHERE 
	order_date = STRFTIME('%Y-%m-%D' , DATE(CURRENT_DATE , 'START OF MONTH' , '-1 MONTH'))

```


```sql
SELECT DISTINCT
STRFTIME('%Y-%m', Order_Date) RECORTE_DATA
, order_date #pra validar se tá no lugar certo
FROM Sales
WHERE 
	order_date BETWEEN = STRFTIME('%Y-%m-%d' , DATE(CURRENT_DATE , 'START OF MONTH' , '-1 MONTH'))
	AND STRFTIME('%Y-%m-%d' , DATE(CURRENT_DATE , 'START OF MONTH' , '-1 DAY'))
```

***Resultado:***
![[Dados 7.png]]

Agora só falta fazer a contagem de vendas

```sql
SELECT DISTINCT
COUNT(DISTINCT order_id) QNTD_VENDAS
FROM Sales
WHERE 
	order_date BETWEEN = STRFTIME('%Y-%m-%d' , DATE(CURRENT_DATE , 'START OF MONTH' , '-1 MONTH'))
	AND STRFTIME('%Y-%m-%d' , DATE(CURRENT_DATE , 'START OF MONTH' , '-1 DAY'))
```

***Resultado:***

| QNTD_VENDAS | |
|------------------|-|
| 67 | |

> [!TIP] 
> USE VARIÁVEIS, não o valor "na pedra"

***Contexto:***
- Qual a evolução mês a mês desde que começamos nossas operações?

```sql
SELECT
STRFTIME('%Y-%m', order_date) ANO_MESA
FROM Sales
GROUP BY STRFTIME('%Y-%m', order_date)
ORDER BY ANO_MES DESC
```
***Resultado:***
![[Dados 8.png]]

***Desafios:***
- Quais são as 8 subcategorias que venderam mais de 10 e menos de 100 produtos em 2022?
- Quanto eles somam em valor de venda?

- Crie uma marcação para "de 10 a 50 produtos vendidos" e outra "de 50 a 100 produtos vendidos".

***Quero mais:***
Tech on the net

--- 
## Módulo 4 - Processo de ETL com SQL
--- 
> E = Extract
> T = Transform
> L = Load

>  55% dos líderes não confiam nas respostas dos dados que recebem

\ - Experian, 2021

Nessa mesma pesquisa, 8 em cada 10 desses gestores, estavam contratando pessoas para resolver esse problema.

---
##### ***Missão:*** aprender a fazer ETL em suas bases para aumentar a confiabilidade da sua análise

---
### Importação de dados e enriquecimento de informações

***Contexto:***
- Tu é um freelancer e uma empresa te contrata e envia duas planilha, só que para garantir a proteção dos dados, vc vai usar a coluna ID que eles criaram para conseguir usar as informações entre as planilhas.
![[Estrutura das planilhas.png]]

***Simplificando:***
- Quais são os 1000 melhores clientes que podemos oferecer empréstimo para ação da próxima semana?

*Obs: dessa vez em vez de usar o **Run** vamos usar o **Run & Show Code** porque aí vamos ver a estrutura do `CREATE TABLE`*  

Tu seleciona quando vai importar o arquivo

> [!warning] A partir daqui, eu fiquei de saco cheio

![[Pasted image 20230806184940.png]]


![[Pasted image 20230806185017.png]]
> [!warning] Tem caroço no angu.
> 3 clientes de 144 anos? Tem com certeza algo errado.


Pra juntar as duas:
```sql
SELECT *
FROM pessoas P
LEFT JOIN historico_emp H
ON P.ID = H.ID
```

Dá isso aí:
![[Pasted image 20230806185330.png]]
Eu preciso especificar aqui algo diferente de asterisco?
Sim.
O ID veio duas vezes e não pode isso. Por que não pode ter uma coluna com o mesmo nome em tabelas diferentes?
Porque pra simplificar minha análise eu preciso criar uma tabela temporária, porque se não toda vez que eu for fazer a busca eu vou precisar fazer um `LEFT JOIN`

```SQL
CREATE TEMPORARY TABLE ANALISE AS
SELECT 
P.*
, H.motivo_emp
, H.valor_emp
, H.tx_emp
, H.emp_ativo
FROM pessoas P
LEFT JOIN historico_emp H
ON P.ID = H.ID
```

Depois é só:

```SQL
SELECT * FROM ANALISE
```

> [!TIP] 
> Não faça alterações diretamente na sua fonte

Faça uma cópia, tabela temporária. Sempre tenha os dados fonte. Mesmo depois de tudo.

--- 
### Validação dos dados

***Contexto:***
- Quais são os 1000 melhores clientes que podemos oferecer empréstimo para a ação da próxima semana?

Da última vez tinham dados estranhos, como a idade de 144 com alguns clientes. Nós vamos validar essas informações usando ***Funções de agregação*** e o `WHERE` 

> "Nesses casos é legal ter um bloco de comentário"

Os dois jeitos são: 

`/*comentário*/` ou `--comentário`

```sql
/**/
SELECT 
MIN (IDADE) MENOR_IDADE
, MAX (idade) MAIOR_IDADE
, MIN (anos_trabalho_atual) MENOR_TRABALHO_AT
, MAX (anos_trabalho_atual) MAIOR_TRABALHO_AT

FROM ANALISE
```

![[Pasted image 20230806191227.png]]
Tá estranho pra krl isso aí, tem que ver direito

```SQL
/*
MENOR_IDADE E MENOR_TRABALHO_AT OK
MAIOR_IDADE E MAIOR_TRABALHO_ATUAL TEM INFORMAÇÕES COM IDADES ACIMA DE 100 ANOS - NÃO CONFIAR NESSE DADO
*/`
```

Agora vamos buscar quais clientes não temos dados de empresa, de empréstimos
 ```SQL
SELECT * 
FROM ANALISE
wHERE analise.motivo_emp IS null AND analise.valor_emp IS null AND tx_emp IS null AND emp_ativo IS NULL
```

![[Pasted image 20230806191805.png]]
São os clientes que não temos dados da empresa. 

Aí agente faz um `COUNT` geral pra saber quantos que deu 238
E depois complementa os comentários:

```SQL
/*
MENOR_IDADE E MENOR_TRABALHO_AT OK
MAIOR_IDADE E MAIOR_TRABALHO_ATUAL TEM INFORMAÇÕES COM IDADES ACIMA DE 100 ANOS - NÃO CONFIAR NESSE DADO
238 clientes sem informção de histórico de empréstimos
*/`
```

Agora vamos busca

Quais são as colunas que tem o dado de contato do meu cliente?
`dados_contato


```sql
SELECT COUNT *
FROM ANALISE
WHERE dados_contato = 0
```

```SQL
/*
MENOR_IDADE E MENOR_TRABALHO_AT OK
MAIOR_IDADE E MAIOR_TRABALHO_ATUAL TEM INFORMAÇÕES COM IDADES ACIMA DE 100 ANOS - NÃO CONFIAR NESSE DADO
238 clientes sem informção de histórico de empréstimos
25.805 clientes sem dados de contato
*/`
```


```sql
SELECT COUNT *
FROM ANALISE
WHERE dados_contato = 1
AND idade BETWEEN 18 AND 60
```

Deu:

| `COUNT(*)` |  |
|-----------|-|
| 5520 | |

***Conclusão:***
Comunicar a empresa com:
Deu menos do que 10000 clientes, talvez devessem investir mais em enriquecimento de dados. Para eles atualizarem as informações.

![[Pasted image 20230806193247.png]]
Achamos os caras com 40% lê e tenta entender 40% de quê


![[Pasted image 20230806193523.png]]
Tenho 30 mil pessoas

```
/*
MENOR_IDADE E MENOR_TRABALHO_AT OK
MAIOR_IDADE E MAIOR_TRABALHO_ATUAL TEM INFORMAÇÕES COM IDADES ACIMA DE 100 ANOS - NÃO CONFIAR NESSE DADO
238 clientes sem informção de histórico de empréstimos
25.805 clientes sem dados de contato
30766 clientes
*/
```


---
###  Reconstrução e padronização dos dados
*Vamos usar o `SET UPDATE`  e o `WHERE` pra conseguir alterar as informações que não vemos nenhum sentido. O `SET UPDATE` PRECISA ser usado com o `WHERE`*

Vamos ignorar os clientes com idade maiores do que 60 anos (aposentados). Vamos usar o sub query também

```SQL
UPDATE ANALISE
SET.IDADE = (SELECT AVG(IDADE) FROM ANALISE WHERE IDADE BETWEEN 18 AND 60) /*aqui em cima com os () é um exemplo de subquery*/ 
WHERE IDADE IS NULL /* pra não alterar todo mundo */
```
Pega a tabela analise altera a coluna idade colocando a média de idade dos clientes que estão entre 18 e 60 anos, mas só pros clientes que estiverem sem dados.

Apareceu porra nenhuma, porque só tá gravando informação na tabela, não tá selecionando nem consultando nada. ou seja, usando o `SELECT`

vamos mudar os anos trabalhados também
```sql
UPDATE ANALISE
SET.anos_trabalho_atual = (
							SELECT AVG(anos_trabalho_atual) 
							FROM ANALISE 
							WHERE anos_trabalho_atual >= 30 
						  ) 
WHERE anos_trabalho_atual IS NULL
```
garantimos que as informações de idade e anos de trabalho atual TERÃO dados. Ignoramos informações não tão confiáveis.

Vamos usar o `DELETE` pra apagar os dados que não queremos

> [!TIP] 
> Faça sempre um `SELECT` antes de fazer `SET UPDATE` ou `DELETE` pra garantir que não vai apagar nenhuma informação primordial

Vamos apagar os dados que REALMENTE não confiamos que no caso são: 
- Os clientes que tem dados acima de 99 anos 
- E clientes que tem trabalho mais de 40 anos

```SQL
DELETE FROM ANALISE
WHERE anos_trabalho_atual > 40
OR idade > 99
```

Nossa base está padronizada e limpa

---
### Remoção de duplicados e entrega diferenciada

Vamos usar o `CASE WHEN `para marcar os clientes ideais para a campanha. O que seriam os clientes ideais? Nesse caso, estamos fazendo análises simples, como se possuem e-mails, dados de contato e etc. Quando for trabalhar em outros lugares, terá outros tipos de variáveis e dados.

```sql
SELECT *
, CASE WHEN dados_ contato = 1 AND anos_hist_credito >= 2  
	THEN 1 ELSE 0 END
FROM
```


![[Pasted image 20230806201019.png]]
fds vai bugado mesmo

Vamos entregar todos os critérios como ideal, separados. Para dar liberdade para a empresa decidir oq fazer com a equipe de marketing

![[Pasted image 20230806201610.png]]

Agora ela vai querer meter uma subquery acima do SELECT e 

***Parte de cima do código***
![[Pasted image 20230806201736.png]]

***Parte de baixo do código:***
![[Pasted image 20230806201823.png]]

Agora pra ver se não tem duplicação a gente vai usar a coluna ID

Ela colocou SELECT ID, COUNT * QTDE na primeira linha lá
E um `GROUP BY ID`,
`ORDER BY 2 DESC`

![[Pasted image 20230806202231.png]]

A gente pode ver que todos as colunas selecionadas no `WHERE` nenhuma delas tinha dados duplicados. Não significa que em toda base não tenha. Já que não tem duplicado, vamos apagar o `WHERE`

A tabela final é `SELECT *` na primeira linha e a apagou o `GROUP BY` e o `ORDER BY`

Acima da primeira linha ela coloca um
`CREATE TABLE ANALISE_FINAL AS` (todo o resto do código)

Se você for exportar os dados, vai dar nada, porque é só um banco de testes


Uma forma PIKA de entregar os dados seria com Power BI

Cabô graças a Deus
NÃO TEM MAIS (carinha de choro)

***Desafio:***
- Encontre uma base no site Kaggle que tenha mais de uma planilha e realize todas as etapas que aprendemos até aqui

******

---
#linguagens 
