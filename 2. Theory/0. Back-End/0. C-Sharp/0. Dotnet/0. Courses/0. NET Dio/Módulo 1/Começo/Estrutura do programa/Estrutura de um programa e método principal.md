
#### Arquivos de Projeto

- `.csproj`: Contém informações referente a um projeto (build, debug, versão)
- `.sln` (Solution): Contém informações que carregam um agrupamento de projetos 
	
	![[Pasted image 20240823133306.png]]
	- Como não é ideal que tenhamos uma classe `ContaCorrente` para cada projeto, nós criamos uma terceira classe que contenha ela e "Divida" com os outros projetos.

#### Criando nosso novo projeto

##### Criando uma solution:

1. Instale a extensão: *`vscode-solution-explorer`*
2. Crie uma nova solution
	- Ela vai jogar sozinha, isso aqui no terminal pra você
		```C#
			PS C:\Users\johnn\Desktop\NetDio> dotnet new sln -n "NetDio"
			O modelo "Arquivo de Solução" foi criado com êxito.
			
			PS C:\Users\johnn\Desktop\NetDio> cd "c:\Users\johnn\Desktop\NetDio"
			PS C:\Users\johnn\Desktop\NetDio> dotnet new sln -n "NetDioFundamentos"
			to.
		```
	
3. O VSCode recomenda instalar essa aqui em vez do outro: *`C# Dev Kit - Microsoft`* 

##### Adicionando um projeto existente

- Ele joga isso no terminal depois de vc selecionar as paradas lá:
	```C#
			dotnet sln "c:\Users\johnn\Desktop\NetDio\NetDioFundamentos.sln" add "c:\Users\johnn\Desktop\NetDio\NetDio.csproj"
			O projeto ‘NetDio.csproj’ foi adicionado à solução.
	```
- Depois disso, ele criou dentro do arquivo da `sln`, uma ligação com o projeto existente, que chamamos de referência.

---
##### Criando um novo projeto

- Selecione "add new file project" ou algo assim 
	- Aqui pode dar pau por causa das várias versões de sdk que existem no computador. Então pra contornar isso, você vai colocar isso aqui no prompt:
		```C#
			dotnet new classlib -o MinhaSolucao/MeuProjeto --framework net6.0
		```
		Ou
		```C#
			dotnet new classlib -o Caminho/MeuProjeto --framework net6.0
		```
	#fix-bug
- Selecione oq vc quer criar
	- Nesse caso, foi *"Class Library"*  - `classlib`
- Dê um nome e coloque "`.common`" no final para que seja referenciado por diversos outros, nesse caso, pode ser o mesmo do seu projeto.

---
#### Organizando e referenciando projetos

Depois de criada a solution e referenciado os novos projetos à ela. É necessário organizar os arquivos e as pastas para que elas fiquem assim:

![[Pasted image 20240824131700.png]]

- Jogamos o projeto `NetDio` para dentro da pasta `NetDio`
	- arquivos: 
		- csproj
		- obj
		- cs
		- bin
		- .vscode
- Tiramos a pasta `Models` de `NetDio` e jogamos para a `NetDio.Common`
	- Depois ajustamos os `namespaces` nas classes de `NetDio.Models` para `NetDio.Common.Models`, para melhorar a organização.
- E por final, referenciamos o projeto `Common` dentro do projeto `NetDio`
	```C#
		dotnet add "c:\Users\johnn\Desktop\NetDio\NetDio\NetDio.csproj" reference "c:\Users\johnn\Desktop\NetDio\NetDio.Common\NetDio.Common.csproj"
	```
	- Dá pra fazer isso pela extensão que instalamos também, clicando com o botão direito em qual projeto queremos fazer a referenciação do outro.

---
#### NET5 vs NET6

Para instalar um projeto com uma versão anterior, rode:
```C#
	dotnet new console --framework net5.0
```

##### Comparando os dois:

NET6
```C#
	Console.WriteLine("Hello, world!");
```

NET5
```C#
	using System;
	
	namespace NetDio.NET5
	{
		class Program
		{
			static void Main(string[] args)
			{
				Console.WriteLine("Hello, World!");
			}
		}
	}
```
Do NET5 pra baixo, a gente tem essa estrutura meio diferente e o método `Main()`

- Daria pra dar um `crtl + a` tudo no NET5 e jogar pro NET6 que daria pra rodar de boa, mas não é necessário. Ele já fica implícito no programa

#### Questões

- Em todo projeto .NET, existe um método importante que inicia a execução de nosso código, sendo o ponto de entrada. Esse método é o:
	- Main

- Um projeto pode conhecer outro projeto para usar suas classes, permitindo assim reaproveitar nosso código. Quando um projeto precisa conhecer o outro, chamamos de:
	- Referencia

- Existe um arquivo que organiza e agrupa nossos projetos (.csproj). Esse arquivo é conhecido como:
	- Solution (`.sln`)

- O comando "dotnet run" executa um projeto .NET, buscando por um arquivo em específico. Estamos falando do arquivo:
	- `.csproj`


### Exemplo de estruturação de um projeto .NET

- `../desktop/dionet/nome.csproj`
	```xml
	<Project Sdk="Microsoft.NET.Sdk">
		
		<PropertyGroup>
			<OutputType>Exe</OutputType>
			<TargetFramework>net8.0</TargetFramework>
			<ImplicitUsings>enable</ImplicitUsings>
			<Nullable>enable</Nullable>
		</PropertyGroup>
		
	</Project>
	```
	
	---
	
	- `<OutputType>`
		```xml
		<OutputType>Exe</OutputType>
		```
		Tipo de saída, pode ser ***executável** (Exe)* ou de ***bibliotecas*** *(apenas classes que auxiliam um outro programa executável)*
	
	- `<TargetFramework>`
		```xml
		<TargetFramework>net8.0</TargetFramework>
		```
		Indica a versão que estamos usando
	
	- `<ImplicitUsings> & <Nullable>`
		```xml
		<ImplicitUsings>enable</ImplicitUsings>
		<Nullable>enable</Nullable>
		```
		São metadados que descrevem e indicam como seu projeto deve se comportar, são basicamente opções do seu projeto

---

- `bin`
	- Pasta de binários
	- Depois que compilarmos nosso projeto, ele vai jogar o código compilado em binário *(exe)* pra essa pasta
- `obj` 
	- Não mexemos, é referente a arquivos de debug e compilação
	- Várias pastas
		- Quais são os projetos carregados
		- Path pros pacotes do `nuget`
		- Quais são os arquivos de saída
			- Ou seja, quando compilarmos, ele vai jogar pra pasta `obj`
- `nome.csproj`
	- Estrutura/Configurações de como ela vai se comportar
		- Tipo de saída
		- Versão
		- Metadados
- `Program.cs` 
	- Classe/arquivo que representa o ponto de entrada do nosso projeto C# 

*Obs: Não precisamos guardar as duas primeiras pastas (`bin` & `obj`) porque novas são criadas quando compilamos o projeto com `dotnet build`* 

*Obs2: Também dá pra ter um arquivo de `config` do projeto com a extensão `.json ` (`config.json`)*

==Tem casos em que você pode ter mais de um projeto por repositório, nesse caso, você teria uma ***"Solution"***==