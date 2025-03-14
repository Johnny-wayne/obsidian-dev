Outras páginas:
	- [[ACID e BASE]]
	- [[Tipos de NoSQL]]


## Bancos de Dados NoSQL: Uma Imersão Profunda

### 1. Introdução:

#### <mark style="background: #FFF3A3A6;">1.1 História dos NoSQL:</mark>

Os bancos de dados NoSQL surgiram na década de 2000 como resposta às limitações dos bancos de dados relacionais (SQL) em lidar com as demandas da [[Web 2.0]], como:

* **Escalabilidade:** A necessidade de lidar com volumes de dados crescentes, usuários e tráfego sem comprometer a performance. Os bancos de dados relacionais tradicionais, com sua estrutura tabular e modelo de transações ***ACID***, enfrentavam dificuldades para escalar horizontalmente (adicionando mais servidores).

* **Diversidade de Dados:** A necessidade de armazenar diferentes tipos de dados, além dos tradicionais dados estruturados (números, texto, datas), como imagens, vídeos, geolocalização, gráficos, etc. O modelo tabular de dados SQL se tornava inflexível para lidar com essa variedade.

* **Agilidade:**  O ritmo acelerado do desenvolvimento web demandava flexibilidade no modelo de dados e agilidade na implementação de novas funcionalidades. Os schemas rígidos e o processo de migração de dados em SQL se tornavam obstáculos.

---
#### 1.2 Diferenças entre NoSQL e SQL:

| Característica | SQL | NoSQL |
|---|---|---|
| **Modelo de Dados** | Tabular (relacional) | Não tabular (chave-valor, documento, etc.) |
| **Esquema** | Estruturado (definido previamente) | Flexível (sem esquema definido ou dinâmico) |
| **Escalabilidade** | Difícil (escalabilidade vertical) | Fácil (escalabilidade horizontal) |
| **Performance** | Pode ser lento para grandes quantidades de dados | Geralmente mais rápido para consultas simples |
| **Transações** | ACID (Atomicidade, Consistência, Isolamento, Durabilidade) | BASE (Basicamente disponível, Soft state, Eventualmente consistente) |
| **Complexidade de Consultas** | Consultas complexas usando SQL | Consultas mais simples, com foco em consultas específicas |
| **Aplicações** | Transações complexas, consistência de dados, dados estruturados | Dados semiestruturados, escalabilidade horizontal, agilidade |

---
#### 1.3 Conceitos Essenciais:

* **Escalabilidade:** Capacidade do sistema de lidar com o aumento de dados, tráfego e usuários sem perda de performance.
    * **Escalabilidade Vertical:** Aumento da capacidade de um único servidor (mais RAM, CPU, armazenamento).
    * **Escalabilidade Horizontal:** Adicionando mais servidores para distribuir a carga de trabalho.
* **Schema:** Estrutura dos dados, que define os tipos de dados, relacionamentos e regras de integridade.
    * **Esquemas Estruturados:**  Definidos previamente e rígidos.
    * **Esquemas Dinâmicos:**  Flexíveis, adaptando-se às necessidades dos dados.
* **Performance:** Velocidade e eficiência com que o sistema executa operações como consultas, inserções e atualizações.
* **ACID:** Garante a consistência e integridade dos dados em transações:
    * **Atomicidade:**  Uma transação é executada como um todo, ou não é executada.
    * **Consistência:**  A transação leva o sistema de um estado consistente para outro.
    * **Isolamento:**  As transações são isoladas umas das outras.
    * **Durabilidade:**  Os dados são persistidos permanentemente, mesmo em caso de falhas.
* **BASE:** Mais tolerante a falhas, priorizando a disponibilidade em detrimento da consistência total:
    * **Basicamente disponível:**  O sistema está disponível a maior parte do tempo.
    * **Soft state:**  O sistema pode estar em um estado inconsistente por um curto período.
    * **Eventualmente consistente:**  O sistema eventualmente se torna consistente, mesmo após falhas.

---
### 2. Tipos de Bancos de Dados NoSQL:

#### 2.1 Tipos Gerais:

* <mark style="background: #FF5582A6;">**Column-oriented</mark>:** Armazenam dados em colunas, otimizando consultas por colunas específicas. Cada linha representa uma entidade e as colunas representam seus atributos. São ideais para análises e consultas com filtros em colunas específicas.
    * **Exemplos:** Cassandra, HBase.
    
* <mark style="background: #FFF3A3A6;">**Key-value</mark>:** Armazenam dados como pares chave-valor, simples e rápido para consultas. São ideais para armazenamento de cache, sessões de usuário e dados que são frequentemente acessados.
    * **Exemplos:** Redis, Memcached.
    
* <mark style="background: #FF5582A6;">**Document</mark>:** Armazenam dados em documentos JSON-like, flexíveis para diferentes estruturas. Cada documento representa um objeto com seus atributos e valores. São ideais para armazenamento de dados semiestruturados, como dados de usuários, logs e documentos.
    * **Exemplos:** MongoDB, CouchDB.
    
* <mark style="background: #BBFABBA6;">**Graph</mark>:** Modelam relacionamentos entre entidades, otimizados para consultas complexas. Cada entidade é um nó e as conexões entre elas são representadas por arestas. São ideais para redes sociais, análises de dados e sistemas de recomendação.
    * **Exemplos:** Neo4j, OrientDB.

---
#### 2.2 <mark style="background: #FFF3A3A6;">Tipos Específicos</mark>:

* **Coluna/Família de colunas:** Armazenam dados em colunas, com a possibilidade de agrupar colunas em "famílias". Cada família representa um grupo de atributos relacionados. 
    * **Exemplos:** Cassandra, HBase.
	
* **Chave-valor:**  As chaves são strings únicas e os valores podem ser de qualquer tipo de dados. 
    * **Exemplos:** Redis, Memcached.
    
* **Documento:**  Os documentos podem ter estruturas diferentes, permitindo armazenar dados semiestruturados. 
    * **Exemplos:** MongoDB, CouchDB.


---
### 3. Introdução ao MongoDB e Instalação:

#### 3.1 Introdução ao MongoDB:

* **Características:**
    * **Banco de dados NoSQL de documentos:** Armazena dados em documentos JSON-like.
    * **Flexível:** Permite a criação de documentos com estruturas diferentes e a mudança de estrutura sem afetar outros documentos.
    * **Escalável:** Pode ser facilmente escalado horizontalmente adicionando mais servidores.
    * **Alto desempenho:**  Otimizado para consultas e operações de leitura e escrita.
    * **Linguagem de Consulta Poderoso:**  MongoDB Query Language (MQL) é uma linguagem rica e intuitiva para consultar documentos.
* **<mark style="background: #FF5582A6;">Estruturação</mark>:**
    * **Coleções:** Similar a tabelas em bancos de dados relacionais.
    * **Documentos:** Representam objetos com seus atributos e valores.
    * **IDs:** Cada documento possui um ID único para identificação.
* **Quando Usar:**
    * Armazenamento de dados semiestruturados ou complexos.
    * Aplicações que exigem alta escalabilidade e flexibilidade de dados.
    * ==Desenvolvimento de APIs e microservices.==

---
#### 3.2 Instalação:

* **Tipos de Instalação:**
    * **Localmente:** Instalação em seu servidor.
    * **Cloud:** Instalação em um serviço de nuvem, como MongoDB Atlas.
* **Como Instalar:**
    * **Localmente:**
        * Baixe e instale o pacote do MongoDB para o seu sistema operacional.
        * Configure as configurações necessárias, incluindo a localização do diretório de dados.
        * Inicie o serviço do MongoDB.
    * **Cloud:**
        * Crie uma conta no serviço de nuvem desejado.
        * Configure um cluster de MongoDB.
        * Configure as configurações de segurança e acesso.

---
#### 3.3 MongoDB Cloud:

* **MongoDB Atlas:**  Plataforma de nuvem gerenciada para MongoDB, oferecendo:
    * **Escalabilidade e Disponibilidade:**  Ajuste o tamanho do cluster para lidar com a carga de trabalho.
    * **Segurança e Gerenciamento:**  Criptografia, autenticação e backup automatizados.
    * **Integração com Outros Serviços:**  Integração com outros serviços de nuvem como AWS, Azure e GCP.

---
### 4. Schema Design e Boas Práticas em MongoDB:

#### 4.1 [[Schema Design]]:

* **Embedding:** Incluir documentos relacionados diretamente dentro de outros documentos.
    * **Vantagens:** Simplicidade, performance para consultas relacionadas.
    * **Desvantagens:**  Pode levar a duplicidade de dados, dificuldade em atualizar dados relacionados.
* **Reference:** Criar referências entre documentos, usando IDs ou outros campos.
    * **Vantagens:**  Elimina a duplicidade de dados, facilita a atualização de dados relacionados.
    * **Desvantagens:**  Consultas mais complexas, pode haver aumento da latência.

---
#### 4.2 <mark style="background: #FF5582A6;">Boas Práticas</mark>:

* **Definir um Schema:**  Mesmo com a flexibilidade do MongoDB, definir um schema claro ajuda na organização, consistência e manutenção dos dados.
* **Utilizar IDs:**  Definir IDs únicos para cada documento, facilitando a identificação e o gerenciamento de dados.
* **Normalizar os Dados:**  Evite duplicidade de dados, otimizando o espaço de armazenamento e a performance.
* **Usar Índices:**  Melhore a performance das consultas indexando campos específicos.
* **Usar Transações (Quando Necessário):**  Em alguns casos, é possível usar transações no MongoDB para garantir a atomicidade e a consistência de operações.

---
#### 4.3 JSON e BSON:

* **JSON (JavaScript Object Notation):**  Formato de troca de dados leve e humano-legível, ideal para comunicação entre aplicações.
* **BSON (Binary JSON):**  Formato binário de dados utilizado pelo MongoDB, com suporte a tipos de dados mais complexos, como arrays, datas e números binários. 

---
### 5. Conceitos na Prática com MongoDB:

#### 5.1 Operações e Manipulação de Dados:

* **CRUD:** Operações básicas de Create (criar), Read (ler), Update (atualizar) e Delete (deletar) documentos.
    * **Criar Documentos:** `db.collection.insertOne()`, `db.collection.insertMany()`.
    * **Ler Documentos:** `db.collection.findOne()`, `db.collection.find()`.
    * **Atualizar Documentos:** `db.collection.updateOne()`, `db.collection.updateMany()`.
    * **Deletar Documentos:** `db.collection.deleteOne()`, `db.collection.deleteMany()`.
* **Consultas:** Realizar consultas complexas usando a linguagem de consulta do MongoDB.
    * **Operadores de Comparação:** `$eq`, `$gt`, `$lt`, `$ne`, `$in`, `$nin`, etc.
    * **Operadores Lógicos:** `$and`, `$or`, `$not`.
    * **Operadores de Projeção:**  `$project` para selecionar campos específicos.
    * **Operadores de Agregação:**  `$group`, `$sort`, `$limit`, `$skip`, etc.
* **Agrupamentos:**  Agrupar documentos com base em critérios específicos.
    * **$group:** Agrupar documentos com base em um campo específico.
    * **$sum`, `$avg`, `$min`, `$max`:  Realizar cálculos em cada grupo.

---
#### 5.2 Performance e Índices:

* **Índices:**  Aceleram as consultas, indexando campos específicos.
    * **Tipos de Índices:**  Índices simples, compostos, únicos, textuais e geoespaciais.
    * **Criação de Índices:**  `db.collection.createIndex()`.
* **Otimização de Consultas:**  
    * **Escrever consultas eficientes:**  Evite usar consultas que exijam varredura de toda a coleção.
    * **Utilizar índices:**  Garantir que as consultas usem os índices adequados.
    * **Usar limitações:**  `$limit` para restringir o número de documentos retornados.
    * **Usar projeções:**  `$project` para selecionar apenas os campos necessários.

---
#### 5.3 Agregações:

* **Agregações:**  Processar e analisar conjuntos de dados, incluindo cálculos, filtragem e agrupamento.
    * **Pipeline de Agregações:**  Sequência de operações de agregação aplicadas aos dados.
    * **Operadores de Agregação:**  `$match`, `$group`, `$project`, `$sort`, `$limit`, `$skip`, `$unwind`, etc.
* **Exemplos de Aplicações:**
    * **Análise de dados:**  Calcular estatísticas, como média, soma e contagem.
    * **Relatórios:**  Criar relatórios personalizados com base em diferentes critérios.
    * **Insights:**  Extrair insights dos dados para tomada de decisão.

---
### 6. Concluindo:

O MongoDB é uma ferramenta poderosa para desenvolver aplicações modernas que exigem alta escalabilidade, flexibilidade e performance. Ao dominar os conceitos e boas práticas, você pode aproveitar ao máximo os recursos do MongoDB para criar aplicações robustas e eficientes. 

