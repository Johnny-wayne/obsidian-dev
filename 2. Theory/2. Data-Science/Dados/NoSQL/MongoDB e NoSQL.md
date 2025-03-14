***Bancos de dados Não-Relacionais***

##### Objetivo do Curso

Introdução ao mundo do NoSQL, apresentar os tipos de bancos de dados NoSQL assim como realizar pequenas operações em alguns deles com ênfase em MongoDB no qual iremos desde sua instalação, opções de uso na nuvem e operações de manipulação de dados.

1. Entender os fatores que levaram a criação dos bancos NoSQL
2. Conhecer as principais diferenças gerais entre os BD SQL e NoSQL
3. Conhecer as características e vantagens do uso do BD NoSQL

#### Introdução

- 1970 - BD Relacional
- 1998 - 1º Introdução NoSQL
- 2009 - Reaparição NoSQL

NoSQL = Not Only SQL

BD NoSQL substitui os BD relacionais?
- Não mf
- É muito comum a utilização simultânea dos dois

###### Diferenças BD Relacional x BD NoSQL

- Escalabilidade
	- Relacionais 
		- verticais:
			- Se precisar aumentar, tem que colocar processador, memória, disco rígido, etc.
		- horizontais:
			- Replicas de dados apenas para leitura. 
			- Sla mano, essa mulher explica mó estranho.
	- NoSQL
		- horizontal
			- Particionando os dados *(sharding)* entre os nós é o mais conhecido.

- Schema: 
	- BD Relacional:
		- tabela
			- linhas
				- colunas
					- PK - FK
	- BD NoSQL
		- não tem regra 

- Performance:
	- Relacional depende do sistema de disco pra performance
	- Não relacional depende do tamanho do cluster e da latência da rede

- Transações
	- BD Relacional - ***ACID***
		- ***A***tomicidade - ou ela é realizada por completo, ou ela não é realizada
		- ***C***onsistência - quando uma transação for concluída, ela vai estar exatamente em conformidade com os schemas pré-definidos
		- ***I***solamento - uma transação nunca vai interferir em outra transação
		- ***D***urabilidade - uma vez que a transação for concluída, o dado chamais será perdido
	- BD NoSQL - ***BASE***
		- ***Ba***sically Available
		- ***S***oft-State
		- ***E***ventually Consistent

---
### Tipos de banco de dados

Principais NoSQL

- MongoDB - Document
- Redis - Key-Value
- Cassandra - Wide-cloumn (orientado a colunas)
- Neo4j - Orientado à grafos

Os principais tipos que existem hoje em dia, são:

- Document Store
- Key-Value Store
- Wide-Column Store
- Graph Store

---
##### Grafos - Neo4j

Cada bola, é um nó. São os dados. Podem ter várias propriedades ou nenhuma. Assim como pode ter uma label (um nome) ou não.
![[Pasted image 20240923222935.png]]
Comum em detecção de fraudes, mecanismos de recomendação, redes sociais, sistemas de arquivo, games...

- O mais BD mais famoso atualmente que lida com grafos é o **Neo4j**

###### Na prática

Agora a gente vai criar uma estrutura de registros que compõem os dados de uma rede social utilizando um sandbox do Neo4j. 
- Ele usa aquela parada do **ACID** lá, indo meio contra oq a gente disse antes. 
- Ele usa a linguagem ***Cypher*** 

Agente criou um Blank Sandbox. Agora vamos simular como se estivéssemos criando uma rede social.

Para criarmos nós e relacionamentos, nós usamos o comando `CREATE`.

- `CREATE (:cliente {name: "Bob Sponja", age: 28, honnies: ['Caça agua-viva, comer hamburguers']})`
	- Added 1 label, created 1 node, set 3 properties, completed after 32 ms.

- `:cliente`
	- Depois dos dois pontos é onde definimos a nossa label. Ela é totalmente opcional, mas é interessante para depois, quando formos fazer nossos match's, nossas buscas, ela é bem utilizada
- `{Aqui dentro vem as propriedades}`

Esse é um tipo de banco de dados totalmente *Schema free*
  
Quando queremos simplesmente criar um nó, esse comando basta

- Consultando
	
	`MATCH (bob_esponja) RETURN bob_esponja;` 
	
	O Neo4j tem algumas formas de apresentação dos dados, o de grafos, fica mais ou menos assim:
	![[Pasted image 20240924174615.png]]
	- Ele também retorna em JSON, texto e código

---
#### Coluna/Familia de colunas
*parece ser o mais chatinho*

![[Pasted image 20240926192608.png]]
A de cima é Relacional a de baixo não.

O mais usado é o Cassandra.

- **Keyspace:** agrupamento de famílias de colunas colunas => database
- **Column Family/table:** agrupamento de colunas => table
- **Row key:** chave que representa uma linha de coluna => Primary Key
- **Column:** representa um valor contendo: Name, Value Timestamp 

Registro de transações: compras, resultados de testes, filmes assistidos e localização mais recentes do filme.
Rastreando praticamente qualquer coisa, incluindo status do pedido pacotes etc.

---
#### Chave-Valor - Redis

![[Pasted image 20240927114358.png]]

Armazena um conjunto de dados, seja ele simples ou complexo, identificados por um identificador exclusivo.

+ + Desempenho em aplicações na nuvem
+ - menor capacidade de busca

Uso: cache, sessão de usuário, carrinhos de compra.

Vamos usar o **Redis** um banco de dados, cache, mensageria e fila
- Alto desempenho
- Estrutura de dados na memória
- Versatilidade de uso
- Replicação e persistência

Quem usa: Twitter, Github, Stack overflow entre outros.

Um recurso legal, é que nós podemos passar um tempo de expiração pra chave, o que serve muito bem para cache e pra sessões de usuários.

---
#### Documento 

Dados e documentos autocontidos e auto descritivos. Permite redundância e inconsistência. Livre de esquemas, podendo utilizar JSON, XML entre outros. Aqui, vamos usar o MongoDB

---
### MongoDB

#### Introdução

- Características
	- Código aberto
	- Alta performance
	- Schema-free
	- Utiliza JSON para armazenamento de dados
	- Suporte a indices
	- Auto-Sharding
	- Map-Reduce
	- GridFS

- Estruturação
	- O documento é a menor unidade que teremos no Mongo, ele indica a instância de uma tupla.
		- Document ==> Tupla/Registro
	- Collection é onde colocaremos todos os nossos documentos, é análoga a tabela do SQL
		- Collection ==> Tabela
	- ==Não entendi muito bem==
		- Embedding/Linking ==> Join

- Quando usar:
	- Grande volume de dados
	- Dados não necessariamente estruturados
	
	- Quando não usar
		- Necessidade de relacionamentos/joins
		- Quando propriedades ACID e transações são importantes
		
		Curiosidade: Diversas entidades de pagamento não homologam sistemas cujos dados financeiros dos clientes não estejam em bancos de dados relacionais tradicionais.

##### Instalando

Com docker:
```yml
version: '3.8'

services:
  db: 
    image: mongo
    container_name: db
    restart: always
    environment: 
      - MONGO_INITDB_ROOT_USERNAME=dio
      - MONGO_INITDB_ROOT_PASSWORD=dio
    ports:
      - "27017:27017"
    volumes:
      - C:/Users/johnn/Desktop/docker-dio/dbdata:/data/db
```
*Se tiver dúvidas, vá a [[Imagens Docker]]*

Depois:
1. `docker-compose up -d` pra iniciar o container.
2. `docker container ps` pra listar os containers e ver se está rodando na porta certa
	1. Se não estiver, provavelmente deu pau com os volumes ou outra parte do compose. Nesse caso, cria outra pasta, e tenta inicializar lá
3. Agora pra operarmos o Mongo, precisamos ter ele instalado localmente, ou usar um GUI como o `Robo 3T`

---
#### Schema Design

Discutimos que os bancos de dados NoSQL são Schema-free, mas isso não significa que não existam boas práticas.

Temos duas formas de modelar nossos dados.

**Embedding vs Referência** 

A mais recomendada é o Embedding
- É nada mais é, do que ter o documento autocontido, todas as informações vão estar dentro dele, sem precisar fazer referências pra outros documentos

Referências
- Por mais que sabemos que referências não são uma boa prática no MongoDB, a literatura mostra que tem como
- MongoDB não tem o conceito de uma Foreign-Key, ou seja, não vamos ter uma Constraint que vai garantir esses relacionamentos, de certa forma, vamos ter atributos que vão fazer referências para outros documentos ou outras colections.

- Embedding vs Referência
	![[Pasted image 20240929134138.png]]
	Eu sei que a imagem tá uma merda, mas esse curso é meio paia

- Embdding:
	- Prós:
		- Consulta informações em uma única Query
		- Atualiza o registro em uma única operação
	- Referência
		- Limite de 16 MB por documento

- Referência
	- Prós:
		- Documentos pequenos 
		- Não duplica informações - (Não é necessariamente ruim)
		- (usando quando os dados não são acessados em todas as consultas)
	- Contras:
		- Duas ou mais Queries ou utilização do $lookup (que é um comando do Mongo aí)

Recomendações de acordo com os relacionamentos:
- One-to-one: prefira atributos chave-valor no documento
	![[Pasted image 20240929134643.png]]
- One-to-few: prefira embedding
	![[Pasted image 20240929134739.png]]
- One-to-many e many-to-many: prefira referência


#### Boas práticas

- Evite documentos muito grandes
- Use nome campos objetivos e curtos
- Analise as suas queries utilizando `explain()`
- Atualize apenas os campos alterados
- Evite negações em queries
- Listas/Arrays dentro dos documentos não podem crescer sem limite, pode ferrar a performance

#### JSON vs BSON

BSON é como o MongoDB armazena nossos dados

- É uma serialização codificada em binário de documentos semelhantes a JSON
- Contém extensões que permitem a representação de tipos de dados que não fazem parte da especificação JSON. Por exemplo, BSON tem um tipo `Date`, `ObjectID`.

#### Operações de manipulação de dados

O database é composto por *collections* e essas *collections* são compostas por *documentos.*

Existem duas formas para criarmos nossas collections:
- Uma delas é explicitamente. Vamos executar um comando que vai ser responsável por criar uma *collection*
	- Quando você cria de forma explicita você consegue passar alguns validadores pra ele, como por exemplo, o tamanho máximo do documento, tamanho máximo da *collection*, números máximos de documentos
- Já o outro, nós vamos usar diretamente o nome da nossa *collection* e o Mongo vai saber, se não existir ainda, ele vai criar.

