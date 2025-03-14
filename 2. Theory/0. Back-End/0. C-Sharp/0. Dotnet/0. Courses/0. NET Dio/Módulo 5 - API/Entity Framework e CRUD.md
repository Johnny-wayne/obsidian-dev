
#### Introdução

O EF (Entity Framework) é um framework ORM (Object-Relational Mapping) criado para facilitar a integração com o banco de dados, mapeando tabelas e gerando comandos SQL de forma automática.

Até agora, trabalhamos com [[Dados em memória]] e agora queremos trabalhar com [[Dados em persistência]]. Ou seja, vamos pegar os dados, jogar pra uma API pra ela jogar pro banco de dados.

![[Pasted image 20241008134423.png]]

- ***UI (User Interface)*** - Onde interagimos com o cliente.
- ***Business Layer*** - Classes, Controllers, dados, processamento e etc.
- ***Data Layer*** - A camada mais próxima do banco de dados. O EF fica aí, ele se comunica com o banco de dados.

Daria pra gente escrever comando na mão com o C# pra falar com DB, mas o EF faz isso pra gente.

---
#### CRUD
O acrônimo ***C.R.U.D***. significa:

- ***C*** - CREATE (Insert)
- ***R*** - READ (Select)
- ***U*** - UPDATE (Update)
- ***D*** - DELETE (Delete)

Aonde vc ver que tem CRUD, normalmente está fazendo integração com o DB.

---
#### Instalando pacotes

```bash
dotnet tool install --global dotnet-ef
```
*Instalando o Entity Framework... (Só precisa instalar a ferramenta uma vez)*

```bash
dotnet add package Microsoft.EntityFrameworkCore.Design
```
Esse pacote aqui precisa instalar em todo projeto

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```
Esse também...

Se der problema de versão:
```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 6.0.5
```
#fix-bug 