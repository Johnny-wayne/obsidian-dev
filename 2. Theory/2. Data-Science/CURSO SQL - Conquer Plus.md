## Módulo 1 - Básico

### Softwares de SQL:

- SQLite
- Microsoft SQL Server
- MySQL
- PostgreSQL
- Google Big Query
- SAP Hana Studio

---
### Estrutura de Informações

Uma tabela possui:

- Colunas (campos)
- Linhas (informações)

Cada linha contém informações de cada coluna.  Uma planilha equivale a uma tabela.

**Exemplo de Colunas:** Idade, Nome, Endereço

**Exemplo de Linhas:** 23, Bia, Campinas

---
### Usando SQLite Online (3 tabelas: Product, Sales, Customers)

### Primeiras Queries

- `SELECT`: Especifica as colunas a serem exibidas.
- `FROM`: Especifica a tabela de origem.

> **Contexto:**  Selecione os dados dos produtos mais caros.

Use `*` entre `SELECT` e `FROM` para selecionar todos os campos.

```sql
SELECT * FROM Product; 
```

```sql
SELECT product_name, price FROM Product ORDER BY price DESC;
```

`ORDER BY price DESC`: Ordena os resultados em ordem decrescente de preço.  O padrão é crescente.

```sql
SELECT product_name, price FROM Product ORDER BY price DESC LIMIT 5;
```

`LIMIT 5`: Limita o resultado a 5 linhas.  (Pode ser `TOP 5` em outros bancos de dados).

---
### Selecionando Informações Específicas (Usando WHERE)

> **Contexto:** Dentro da categoria "Tecnologia", liste os 15 produtos mais baratos com valor acima de R$10 ou que sejam acessórios.

`WHERE`: Filtra os resultados.

| Operador     | Descrição         |
| ------------ | ----------------- |
| `=`          | Igual             |
| `!=` ou `<>` | Diferente         |
| `<=`         | Menor ou igual    |
| `>=`         | Maior ou igual    |
| `>`          | Maior             |
| `<`          | Menor             |
| `BETWEEN`    | Intervalo         |
| `IN`         | Lista de valores  |
| `NOT IN`     | Não está na lista |
| `LIKE`       | Busca aproximada  |

Use aspas simples para texto.

```sql
SELECT * FROM Product WHERE category = "Technology";
```

>[!tip] 
>Use `UPPER` ou `LOWER` para padronizar a comparação de texto (maiúsculas/minúsculas).
```sql
SELECT * FROM Product WHERE lower(category) = "technology";
```

> [!failure] 
> - Aspas simples ('Text') podem não funcionar em todos os bancos de dados; aspas duplas ("Text") podem ser necessárias.

`AND` e `OR`: Combinam condições.

```sql
SELECT * FROM Product WHERE lower(category) = "technology" AND (price > 10 OR lower(sub_category) = "accessories") ORDER BY price LIMIT 15;
```

> [!todo] 
> - **Desafio:** Liste os 10 produtos mais caros fora da categoria "Tecnologia", com valor máximo de R$1.000.

**Resultado:**

```sql
SELECT * FROM Product WHERE lower(category) != "technology" AND price <= 1000 ORDER BY price DESC LIMIT 10;
```

---
## Módulo 2 - Intermediário

### Trabalhando com Agregações: COUNT, SUM, MAX, MIN, AVG

> **Contexto:**  Informações sobre o catálogo da Conquer Sales: quantidade de produtos, média de preços, maior e menor preço.

| Função | Descrição |
|---|---|
| `COUNT` | Conta o número de linhas (ou valores distintos com `DISTINCT`). |
| `AVG` | Calcula a média. |
| `MAX` | Retorna o maior valor. |
| `MIN` | Retorna o menor valor. |
| `SUM` | Soma os valores. |

```sql
SELECT COUNT(*) AS TOTAL_LINHAS, COUNT(DISTINCT product_id) AS TOTAL_PRODUTOS FROM Product;
```

> [!warning] 
>- `COUNT(product_id)` conta as ocorrências, mesmo as repetidas. Use `COUNT(DISTINCT product_id)` para contagem sem repetições.

```sql
SELECT COUNT(*) AS TOTAL_LINHAS, COUNT(DISTINCT product_id) AS TOTAL_PRODUTOS, AVG(price) AS MEDIA_VALOR, MAX(price) AS MAIOR_VALOR, MIN(price) AS MENOR_VALOR FROM Product;
```

---
### Trabalhando com Agregações: GROUP BY e DISTINCT

```sql
SELECT category FROM product GROUP BY category;
```

ou

```sql
SELECT DISTINCT category FROM product;
```

```sql
SELECT category, COUNT(*) AS TOTAL_LINHAS, COUNT(DISTINCT product_id) AS TOTAL_PRODUTOS, AVG(price) AS MEDIA_VALOR, MAX(price) AS MAIOR_VALOR, MIN(price) AS MENOR_VALOR FROM Product GROUP BY category;
```

**Ordem das Queries:** `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `ORDER BY`, `LIMIT` (LIMIT não funciona em todos os bancos de dados).

>**Contexto:** Top 8 subcategorias com preços entre R$10 e R$1000, ordenadas pelo valor médio.

```sql
SELECT sub_category, category, SUM(price) valor_total, AVG(price) valor_medio FROM Product WHERE price BETWEEN 10 AND 1000 GROUP BY sub_category, category ORDER BY valor_medio LIMIT 8;
```

>[!tip] 
>Em bases grandes ou em nuvem, use `LIMIT` para otimizar a performance.

---
### Enriquecendo sua base: LEFT JOIN

>**Contexto:** Top 5 produtos e quantidade de vendas de cada.

`LEFT JOIN`: Junta tabelas, mantendo todas as linhas da tabela da esquerda.

```sql
SELECT P.product_name, P.price, COUNT(DISTINCT S.order_id) QNT_VENDAS FROM Product P LEFT JOIN Sales S ON S.product_id = P.product_id GROUP BY P.product_name, P.price ORDER BY price DESC LIMIT 5;
```

> [!note] 
>- Valores não encontrados na tabela da direita serão `NULL`.

>**Contexto:** 10 cidades com menos vendas.

```sql
SELECT c.city, COUNT(DISTINCT S.order_id) qntd_vendas FROM Sales S LEFT JOIN Customer C ON S.customer_id = C.customer_id GROUP BY C.city ORDER BY 2 LIMIT 10;
```

>[!note] 
>`COUNT` requer `GROUP BY`.


---
### Outros Tipos de JOIN

![[SQL.png]]

> **Contexto:** Clientes que compraram em abril (campanha de marketing).

```sql
SELECT S.*, CA.city FROM Sales S INNER JOIN campaign ca ON CA.Custommer_id = S.Customer_id WHERE S.Order_Date LIKE '2022-04%';
```

> [!tip] 
> - Consultas otimizadas melhoram a performance.


---
## Módulo 3 - Indo Além

### CASE WHEN

```sql
CASE WHEN condição1 THEN resultado1 WHEN condição2 THEN resultado2 ELSE resultado3 END
```

> **Contexto:** Número de categorias com produtos na cor cinza.

```sql
SELECT category, product_name, CASE WHEN UPPER(product_name) LIKE "%GRAY%" THEN 'SIM' ELSE 'NAO' END AS VALIDADOR, COUNT(DISTINCT category) AS QNTD_VENDAS FROM Product GROUP BY VALIDADOR;
```

> **Contexto:** Agrupando categorias ("Furniture", "Office Supplies", "Outros") e contando produtos com a cor cinza.

```sql
SELECT CASE WHEN UPPER(category) IN ('OFFICE SUPPLIES', 'FURNITURE') THEN category ELSE 'Others' END tipo_categoria, SUM(CASE WHEN UPPER(product_name) LIKE "%GRAY%" THEN 1 ELSE 0 END) AS VALIDADOR FROM Product GROUP BY tipo_categoria;
```

---
### HAVING

> **Contexto:** Estados com entre 30 e 100 vendas.

`HAVING`: Filtra resultados após o `GROUP BY`.

```sql
SELECT C.State, COUNT(DISTINCT S.Order_ID) QTDE FROM sales S LEFT JOIN customer C ON S.customer_id = C.customer_id GROUP BY C.State HAVING QTDE BETWEEN 30 AND 100;
```

> [!tip] 
>- `WHERE`: filtra antes do `GROUP BY`; `HAVING`: filtra depois.

---
### Otimização de Consultas: SUBQUERY & TEMPORARY TABLE

> **Contexto:** 3 cidades com maior valor de venda em "Tecnologia" na Califórnia.

**SUBQUERY:**

```sql
SELECT C.city, COUNT(DISTINCT S.Order_ID) QTDE FROM Sales S INNER JOIN (SELECT * FROM product WHERE category = "Technology") P ON S.Product_ID = P.product_id INNER JOIN (SELECT * FROM customer WHERE state = "california") C ON C.customer_id = S.customer_id GROUP BY c.city ORDER BY 2 DESC LIMIT 3;
```

**TEMPORARY TABLE:**

```sql
CREATE TEMPORARY TABLE p AS SELECT * FROM product WHERE category = "Technology";
CREATE TEMPORARY TABLE C AS SELECT * FROM customer WHERE state = "california";
SELECT C.city, COUNT(DISTINCT S.Order_ID) QTDE FROM Sales S INNER JOIN P ON S.Product_ID = P.product_id INNER JOIN C ON C.customer_id = S.customer_id GROUP BY c.city ORDER BY 2 DESC LIMIT 3;
DROP TEMPORARY TABLE p;
DROP TEMPORARY TABLE C;
```

> [!tip] 
> - Compare o tempo de execução para escolher entre `SUBQUERY` e `TEMPORARY TABLE`.

---
### Análise de Datas: DATE & SUBSTR

- `CURRENT_DATE`: Data atual.
- `DATE()`: Data no formato AAAA-MM-DD.
- `STRFTIME`: Formata datas.

> **Contexto:** Vendas do mês passado.

```sql
SELECT COUNT(DISTINCT order_id) QNTD_VENDAS FROM Sales WHERE order_date BETWEEN STRFTIME('%Y-%m-%d', DATE('now', '-1 month', 'start of month')) AND STRFTIME('%Y-%m-%d', DATE('now', '-1 day'));
```

> **Contexto:** Evolução mês a mês das vendas.

```sql
SELECT STRFTIME('%Y-%m', order_date) ANO_MES, COUNT(*) AS VENDAS FROM Sales GROUP BY ANO_MES ORDER BY ANO_MES DESC;
```

---
## Módulo 4 - Processo de ETL com SQL

#### Importação de Dados e Enriquecimento de Informações

(Descrição do processo de importação e junção de dados das planilhas "pessoas" e "historico_emp", usando `CREATE TEMPORARY TABLE` para facilitar a análise.)

#### Validação dos Dados

(Análise de dados inconsistentes (idades e anos de trabalho), usando `MIN`, `MAX`, e `WHERE` para identificar problemas.)

### Reconstrução e Padronização dos Dados

(Utilização de `UPDATE` e `WHERE` para corrigir dados inconsistentes em idade e anos de trabalho, e `DELETE` para remover dados não confiáveis.)

### Remoção de Duplicados e Entrega Diferenciada

(Uso de `CASE WHEN` para classificar clientes ideais, e verificação de duplicatas usando `GROUP BY` e `COUNT`.)

(Descrição da criação da tabela final `ANALISE_FINAL`.)

> [!todo] Desafio: 
> - Encontre uma base de dados no Kaggle com múltiplas planilhas e aplique as técnicas aprendidas.


