# Curso SQL - Conquer Plus: Um Guia Detalhado

Este documento serve como um guia expandido do curso SQL Conquer Plus, detalhando os conceitos-chave e fornecendo exemplos adicionais para reforçar o aprendizado. Ele se concentra nos principais módulos e tópicos abordados, incluindo exemplos práticos e dicas de otimização.

## Módulo 1: Fundamentos de SQL

Este módulo introduz os conceitos básicos do SQL, incluindo diferentes sistemas de gerenciamento de banco de dados (SGBDs), a estrutura das tabelas e as primeiras consultas.

### Sistemas de Gerenciamento de Banco de Dados (SGBDs)

O curso abrange diversos SGBDs, destacando suas características e aplicações:

- **SQLite:** Banco de dados leve e embutido, ideal para aplicações menores e dispositivos móveis. Usado no curso como ambiente de prática. [[SQLite]]
    
- **Microsoft SQL Server:** SGBD robusto e amplamente utilizado em ambientes corporativos.
    
- **MySQL:** SGBD open-source popular, conhecido por sua escalabilidade e flexibilidade.
    
- **PostgreSQL:** SGBD open-source poderoso e conhecido por sua conformidade com os padrões SQL.
    
- **Google BigQuery:** Plataforma de análise de dados em nuvem da Google.
    
- **SAP Hana Studio:** SGBD in-memory da SAP, otimizado para processamento de grandes volumes de dados.
    

### Estrutura de Dados em SQL: Tabelas

As informações em um banco de dados SQL são organizadas em tabelas, que são estruturas bidimensionais compostas por:

- **Colunas (Campos):** Representam as características ou atributos dos dados. Exemplos: Nome, Idade, Cidade, Preço.
    
- **Linhas (Registros):** Representam os itens individuais de dados, com um valor para cada coluna. Cada linha representa uma instância única.
    

Uma analogia útil é uma planilha: as colunas são as cabeças das colunas da planilha, e as linhas são as diferentes entradas de dados.

### Primeiras Consultas SQL

As consultas SQL são utilizadas para recuperar informações de um banco de dados. As consultas mais básicas usam as cláusulas SELECT e FROM.

**SELECT:** Especifica quais colunas você deseja exibir. * seleciona todas as colunas.

**FROM:** Especifica a tabela de onde os dados serão recuperados.

**Exemplo:**

```
SELECT * FROM Product;  -- Seleciona todas as colunas da tabela Product.
SELECT product_name, price FROM Product; -- Seleciona apenas o nome do produto e o preço.
```

content_copydownload

Use code [with caution](https://support.google.com/legal/answer/13505487).SQL

**Ordenando Resultados (ORDER BY):**

A cláusula ORDER BY ordena os resultados de uma consulta. ASC (ascendente) é o padrão, DESC (descendente) ordena do maior para o menor.

**Exemplo:**

```
SELECT product_name, price FROM Product ORDER BY price DESC; -- Ordena os produtos pelo preço, do maior para o menor.
```

content_copydownload

Use code [with caution](https://support.google.com/legal/answer/13505487).SQL

**Limitando Resultados (LIMIT / TOP):**

A cláusula LIMIT (SQLite e muitos outros SGBDs) ou TOP (SQL Server) limita o número de linhas retornadas.

**Exemplo:**

```
SELECT product_name, price FROM Product ORDER BY price DESC LIMIT 5; -- Retorna os 5 produtos mais caros.
SELECT TOP 5 product_name, price FROM Product ORDER BY price DESC; --  (SQL Server) Mesmo resultado.
```

content_copydownload

Use code [with caution](https://support.google.com/legal/answer/13505487).SQL

**Observações sobre o uso de ; (ponto-e-vírgula):** Em alguns SGBDs, como o SQLite usado no curso, o ponto e vírgula não é estritamente necessário para separar as consultas, mas é uma boa prática para manter a clareza do código. Em outros SGBDs, ele é obrigatório.

## Módulo 2: Consultas Intermediárias

Este módulo expande as consultas SQL, incluindo agregações, filtros avançados e junções entre tabelas.

### Agregações: COUNT, SUM, AVG, MAX, MIN

As funções de agregação permitem calcular valores a partir de conjuntos de dados.

- **COUNT(*):** Conta o número total de linhas.
    
- **COUNT(DISTINCT coluna):** Conta o número de valores únicos em uma coluna.
    
- **SUM(coluna):** Soma os valores numéricos em uma coluna.
    
- **AVG(coluna):** Calcula a média dos valores numéricos em uma coluna.
    
- **MAX(coluna):** Retorna o maior valor em uma coluna.
    
- **MIN(coluna):** Retorna o menor valor em uma coluna.
    

**Exemplo:**

```
SELECT COUNT(*) AS TotalProdutos, AVG(price) AS MediaPreco FROM Product;
```

content_copydownload

Use code [with caution](https://support.google.com/legal/answer/13505487).SQL

### GROUP BY e DISTINCT

GROUP BY agrupa linhas com valores iguais em uma ou mais colunas. É frequentemente usado com funções de agregação para calcular valores agregados para cada grupo.

DISTINCT retorna apenas os valores únicos de uma coluna.

**Exemplo:**

```
SELECT category, COUNT(*) AS NumeroProdutos FROM Product GROUP BY category; -- Conta o número de produtos em cada categoria.
SELECT DISTINCT category FROM Product; -- Lista as categorias únicas.
```

content_copydownload

Use code [with caution](https://support.google.com/legal/answer/13505487).SQL

A ordem padrão das cláusulas em uma consulta SQL é: SELECT, FROM, WHERE, GROUP BY, HAVING, ORDER BY, LIMIT.

### Junções (JOIN) entre Tabelas

Junções são usadas para combinar dados de várias tabelas com base em uma coluna comum. O curso cobre diversos tipos de junções:

- **INNER JOIN:** Retorna apenas as linhas que têm correspondência em ambas as tabelas, baseado na condição da junção (ON).
    
- **LEFT (OUTER) JOIN:** Retorna todas as linhas da tabela da esquerda (a que vem antes do LEFT JOIN), e as linhas correspondentes na tabela da direita. Se não houver correspondência, os campos da tabela da direita serão NULL.
    
- **RIGHT (OUTER) JOIN:** Similar ao LEFT JOIN, mas retorna todas as linhas da tabela da direita.
    
- **FULL (OUTER) JOIN:** Retorna todas as linhas de ambas as tabelas.
    

**Exemplo de LEFT JOIN:**

```
SELECT p.product_name, s.order_id
FROM Product p
LEFT JOIN Sales s ON p.product_id = s.product_id;
```

content_copydownload

Use code [with caution](https://support.google.com/legal/answer/13505487).SQL

Este exemplo combina as tabelas Product e Sales usando o product_id como chave. Ele retorna todos os produtos, mesmo aqueles que não têm vendas registradas na tabela Sales.

## Módulo 3: Consultas Avançadas

Este módulo apresenta técnicas avançadas de consultas SQL para análise de dados mais complexa.

### CASE WHEN

A estrutura CASE WHEN permite criar lógica condicional dentro das consultas SQL. Ela avalia condições e retorna diferentes valores com base nos resultados.

**Exemplo:**

```
SELECT product_name,
       CASE
           WHEN price > 100 THEN 'Caro'
           WHEN price > 50 THEN 'Moderado'
           ELSE 'Barato'
       END AS PrecoCategoria
FROM Product;
```

content_copydownload

Use code [with caution](https://support.google.com/legal/answer/13505487).SQL

### HAVING

HAVING é usado para filtrar resultados após o agrupamento (GROUP BY). É diferente do WHERE, que filtra antes do agrupamento. HAVING é usado com funções de agregação.

**Exemplo:**

```
SELECT category, COUNT(*) AS NumeroProdutos
FROM Product
GROUP BY category
HAVING COUNT(*) > 10; -- Mostra apenas as categorias com mais de 10 produtos.
```

content_copydownload

Use code [with caution](https://support.google.com/legal/answer/13505487).SQL

### Subconsultas e Tabelas Temporárias

Subconsultas são consultas aninhadas dentro de outras consultas. Tabelas temporárias são tabelas criadas temporariamente para armazenar resultados intermediários, facilitando consultas complexas. Ambas as técnicas podem melhorar o desempenho e a clareza do código.

### Trabalhando com Datas

O curso apresenta funções para manipular e analisar dados de data e hora. As funções específicas variam dependendo do SGBD, mas geralmente incluem funções para extrair partes da data (ano, mês, dia), calcular diferenças entre datas e formatar datas.

## Módulo 4: ETL (Extract, Transform, Load) com SQL

Este módulo aborda o processo ETL, que envolve extrair dados de diferentes fontes, transformá-los para um formato consistente e carregá-los em um banco de dados. O curso demonstra como realizar essas etapas usando SQL.

### Extração e Importação

O processo começa com a extração de dados de várias fontes (planilhas, arquivos CSV, outros bancos de dados). Em seguida, os dados são importados para o banco de dados SQL usando comandos como CREATE TABLE e INSERT INTO.

### Transformação

Nesta etapa, os dados são limpos, transformados e preparados para análise. Isto inclui:

- **Limpeza de dados:** Lidar com valores ausentes, inconsistências e erros nos dados.
    
- **Padronização:** Transformar dados em um formato consistente (ex: padronizar a formatação de datas).
    
- **Enriquecimento:** Adicionar novas informações aos dados existentes (ex: usando junções com outras tabelas).
    

### Carregamento

Finalmente, os dados transformados são carregados no banco de dados. Isso pode envolver a criação de novas tabelas ou a atualização de tabelas existentes.

## Conclusão

Este guia estendido resume os principais pontos do curso SQL Conquer Plus. A prática consistente é fundamental para dominar o SQL. Explore diferentes SGBDs, crie suas próprias consultas e resolva problemas de análise de dados para aprimorar suas habilidades. Lembre-se de que a otimização de consultas é crucial para o desempenho em bancos de dados de grande escala.