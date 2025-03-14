
### Gerenciador de pacotes

###### O que é um pacote?

Um pacote é um conjunto de códigos úteis, que possibilita o compartilhamento e reuso do código.

 > *(Pequeno projeto que só faz determinada função)*

Podemos compartilhar para outras pessoas e sistemas, e aí eles podem usar esse pacote, ou seja, ao invés de ficamos duplicando o código para cada sistema, podemos simplesmente criar o pacote que faz determinada função e em cada sistema, faço uma referência para esse pacote.

#### Nuget

**Nuget** é um gerenciador de pacotes, que permite desenvolvedores compartilharem códigos e bibliotecas

Quando você criar um pacote, você vai subir ele no Nuget, disponibilizando assim, para outros pessoas usarem. O Nuget é apenas para o .NET, não podemos colocar pacotes Java no Nuget, é incompatível.

###### instalando um pacote pelo VScode

 Nesse caso, vamos instalar o `Newtonsoft.Json`, com o comando:
	`dotnet add package Newtonsoft.Json --version 13.0.1`

Toda referência ao pacote vai ficar no `.csproj`.

- `.csproj`
	```C#
	<Project Sdk="Microsoft.NET.Sdk">
	
	  <PropertyGroup>
	    <OutputType>Exe</OutputType>
	    <TargetFramework>net8.0</TargetFramework>
	    <ImplicitUsings>enable</ImplicitUsings>
	    <Nullable>enable</Nullable>
	  </PropertyGroup>
		
	  // Bem aqui ó:
	  <ItemGroup>
	    <PackageReference Include="Newtonsoft.Json" Version="13.0.1" />
	  </ItemGroup>
	
	</Project>
	```

###### Instalando um pacote pelo Visual Studio
É bem mais gráfico

- Clica com o botão direito no `csproj`
- Clica em *"Manage NuGet Packages"*
- Aí vai abrir 3 abas, clique na *"Browse"*
- Pesquisa, clica e instala

---
### Serialização

##### O que é serialização e deserialização?

>O processo de serializar consiste em transformar objetos em fluxo de bytes para seu armazenamento ou transmissão.

**![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUcb2pp-lsYTs2HASvuXrYCE8MH37sNClXwRiMJV878vFGp9flF5yckZ8B54JgnBj4uF0YBS2QU115TkauMr7QWaSvRObTZzWJINSC-NkXCEIepYtWkxJ9geVp8YbjOSMZgGZtlfSI7Upux9y4vRF_RbwAH1-mWGEB4AwNaTscVcaUSbbd5uYh0=nw?key=WF829V7KoocIcU0umWWS8g)**

###### Serialização

- Serialização = transformar o objeto que instanciamos, mais próximo do objeto que queremos armazenar
	- Ex: Instância da Classe `Pessoa`
		```C#
		Pessoa p1 = New Pessoa();
		```

- Basicamente, deixamos o dado compatível com o lugar onde queremos que ele vá
	- Se quisermos que o objeto se torne um arquivo, então traduziremos o Objeto, no caso seus bytes, para ASCI2 ou UTF8, para que ele seja representado em um arquivo. 

###### Deserialização
*É o processo inverso,  quando,  por exemplo, o Arquivo, vire um Objeto para o programa.*


##### Serialização de Dados

- **JSON**
	- JavaScript Notation Object é um formato de texto que segue a sintaxe do Javascript, muito usado para transmitir dados entre aplicações.
	
	- ***Obs:*** *Não está vinculado ao JavaScript, só tem JavaScript no nome pq lembra a sintaxe do JavaScript*
	
	- Toda linguagem que pode ler e gravar um JSON pode se comunicar, mesmo que sejam tecnologias diferentes.
	
	- Exemplo:
		- Imagem 1
			**![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUf_jGdpBFAUrS8z8c_x5MTIgdHbXylCelgm__m6hYA_7olltbaoluWgVeGqS9uKlv-1wg6SsYMRMIA1-TKkwoeMGFa352f8vCaFknC16aonpSIf56j3kj0eX7K18A-bLqw73DkfA3Lm_QU1otEV0RCBjphvoaggN2xR-eiB5jddkBDE3lKRnww=nw?key=WF829V7KoocIcU0umWWS8g)**
		
	- Começa com abre chaves, fecha chaves, e dentro temos as propriedades do objeto.
	
	- Basicamente, um arquivo de texto que representa um objeto

##### Serialização na prática

Vamos usar o pacote previamente instalado `Newtonsoft.Json`

- **Contexto**
	- **Chefe:** os dados que temos de venda, você precisa enviar para nosso cliente
	- **Cliente:** Eu quero receber esses dados em formato JSON para que o meu TI possa ler esses dados
	- **Tarefa:** Pegar os dados, serializar e enviar

```C#
using project2.Models;
using Newtonsoft.Json;

Venda v1 = new Venda(1, "Material de Escritório", 25.00M);

string serializado = JsonConvert.SerializeObject(v1);
```

```output
{"Id":1,"Produto":"Material de Escritório","Preco":25.00}
```

- Entendendo essa porra
	
	- `JsonConvert` 
		- veio do pacote *Newtonsoft*
	- `JsonConvert.SerializeObject()`
		- Serializa o objeto especificado para uma JSON string
	
	*Ahhh mas como que eu saberia que eu preciso usar esse método?*
	
	**.............Lê a porra da documentação.............**

Se você quiser que fique mais legível o output:

```C#
string serializado = JsonConvert.SerializeObject(v1, Formatting.Indented);
```

- output
	```json
	{
	  "Id": 1,
	  "Produto": "Material de Escritório",
	  "Preco": 25.00
	}
	```

Deixou em formato JSON

###### Escrevendo um arquivo JSON

```C#
// instanciamos um objeto
Venda v1 = new Venda(1, "Material de Escritório", 25.00M);

// serializamos ele
string serializado = JsonConvert.SerializeObject(v1, Formatting.Indented);

// Passamos o path e o objeto serializado
File.WriteAllText("Arquivos/vendas.json", serializado);
```

Output:
![[vendas.json]]

###### Serializando uma coleção

`Program.cs`
```C#
	List<Venda> listaVendas = new List<Venda>();
	
	Venda v1 = new Venda(1, "Material de Escritório", 25.00M);
	Venda v2 = new Venda(2, "Licença de software", 110.00M);
	
	listaVendas.Add(v1);
	listaVendas.Add(v2);
	
	string serializado = JsonConvert.SerializeObject(listaVendas, Formatting.Indented);
	
	File.WriteAllText("Arquivos/vendas.json", serializado);
```

- output
	```json
	[
	  {
	    "Id": 1,
	    "Produto": "Material de Escritório",
	    "Preco": 25.00
	  },
	  {
	    "Id": 2,
	    "Produto": "Licença de Software",
	    "Preco": 110.00
	  }
	]
	```

###### JSON Viewer

Validando um JSON. Nesse caso, sabemos que é válido porque foi serializado a partir de um pacote

[JSON Viewer](https://codebeautify.org/jsonviewer)

**Beautify:** deixa bonitinho e legível.

**Minify:** tira os caracteres desnecessário (quebras de linhas, espaços, etc), deixando o código mais leve, diminuiu pela metade o tamanho no exemplo aqui.

**XML** é um **JSON** das antiga, mais verboso.

###### DateTime em JSON

- `Venda.cs`
	```C#
	public Venda(int id, string produto, decimal preco, DateTime dataVenda)
	{
		Id = id;
		Produto = produto;
		Preco = preco;
		DataVenda = dataVenda;
	}
	public int Id { get; set; }
	public string Produto { get; set; }
	public decimal Preco { get; set; }
	public DateTime DataVenda { get; set; }
	```

- `Program.cs`
	```C#
	DateTime dataAtual = DateTime.Now;
	
	List<Venda> listaVendas = new List<Venda>();
	
	Venda v1 = new Venda(1, "Material de Escritório", 25.00M, dataAtual);
	Venda v2 = new Venda(2, "Licença de software", 110.00M, dataAtual);
	
	listaVendas.Add(v1);
	listaVendas.Add(v2);
	
	string serializado = JsonConvert.SerializeObject(listaVendas, Formatting.Indented);
	
	File.WriteAllText("Arquivos/vendas.json", serializado);
	
	Console.WriteLine(serializado);
	```

- output
	```json
	[
	  {
	    "Id": 1,
	    "Produto": "Material de Escritório",
	    "Preco": 25.00
		"DataVenda": "2024-09-05T20:56:34.2301697-03:00"
	  },
	  {
	    "Id": 2,
	    "Produto": "Licença de Software",
	    "Preco": 110.00
		"DataVenda": "2024-09-05T20:56:34.2301697-03:00"
	  }
	]
	```
	Esse formato do JSON é `ISO 8601`, essa ISO padroniza data entre sistemas

---
### Deserializando um Objeto

Suponha que vc recebeu um arquivo JSON, e você precisa importar esse arquivo em objeto no seu sistema.

1. Primeiro precisamos estudar e mapear o conteúdo JSON
	```json
	[
	  {
	    "Id": 1,
	    "Produto": "Material de Escritório",
	    "Preco": 25.00,
	    "DataVenda": "2024-09-05T20:56:34.2301697-03:00"
	  },
	  {
	    "Id": 2,
	    "Produto": "Licença de Software",
	    "Preco": 110.00,
	    "DataVenda": "2024-09-05T20:56:34.2301697-03:00"
	  }
	]
	```
2. Depois, vamos transforma-lo em uma classe com as propriedades do JSON
	```C#
	public class Venda2
    {
        public int Id { get; set; }
        public string Produto { get; set; }
        public decimal Preco { get; set; }
        public DateTime DataVenda { get; set; }
    }
	```
3. Usar a classe
	```C#
	// Lê o arquivo
	string conteudoArquivo = File.ReadAllText("Arquivos/vendas.json");
	
	// Instancia a variavel listaVenda
	// Usa o método DeserializeObject para 
	// <list<Venda2>> -> formato do objeto
	// conteudoArquivo -> conteúdo para deserializar
	List<Venda2> listaVenda = JsonConvert.DeserializeObject<List<Venda2>>(conteudoArquivo);
	
	foreach (Venda2 venda in listaVenda)
	{
	    Console.WriteLine($"Id: {venda.Id}, Produto: {venda.Produto}, Preço: {venda.Preco}, Data: {venda.DataVenda.ToString("dd/MM/yyyy HH:mm")}");
	}
	```
	
	- Entendendo esta porra
		- `string conteudoArquivo = File.ReadAllText("Arquivos/vendas.json");`
			- Lê o arquivo
		- `List<Venda2> listaVenda`
			- Instancia a variável `listaVenda`
		- `JsonConvert.DeserializeObject`
			-  Usa o método `DeserializeObject` para deserializar o arquivo em objeto
		- `<list<Venda2>>`
			- formato do objeto ao qual será deserializado
		- `(conteudoArquivo)`
			- conteúdo para deserializar
		
	```ouput
	Id: 1, Produto: Material de Escritório, Preço: 25,00, Data: 05/09/2024 20:56
	Id: 2, Produto: Licença de Software, Preço: 110,00, Data: 05/09/2024 20:56
	```

### Atributos
#importante

Se o nome dos atributos estiverem diferentes...
```Json
	[
	  {
	    "Id": 1,
	    "Nome_Produto": "Material de Escritório",
	    "Preco": 25.00,
	    "DataVenda": "2024-09-05T20:56:34.2301697-03:00"
	  },
	  {
	    "Id": 2,
	    "Nome_Produto": "Licença de Software",
	    "Preco": 110.00,
	    "DataVenda": "2024-09-05T20:56:34.2301697-03:00"
	  }
	]
```

...do da classe
```C#
	public class Venda2
	{
		public int Id { get; set; }
		public string Produto { get; set; }
		public decimal Preco { get; set; }
		public DateTime DataVenda { get; set; }
	}
```
Dá ruim, pq o método `DeserializeObject` deserializa o a partir dos atributos

E outra se usarmos `Nome_Produto` como nome da propriedade da classe, estaríamos fugindo da convenção de sintaxe do C#, que é CamelCase.

> ***É aí que entram os ==Atributos==***

```C#
	using Newtonsoft.Json;
	
	namespace project2.Models
	{
	    public class Venda2
	    {
	        public int Id { get; set; }
	        
	        [JsonProperty("Nome_Produto")]
	        public string Produto { get; set; }
	        public decimal Preco { get; set; }
	        public DateTime DataVenda { get; set; }
	    }
	}
```
- O formato de `[atribute]` em cima de uma propriedade ou até de uma classe, simboliza um atributo, eles adicionam uma *metadata*, uma informação adicional à essa propriedade

- `[JsonProperty("Nome_Produto")]`
	- `JsonProperty` que vem do *`Newtonsoft.Json`* é uma classe que está adicionando uma *metadata* (uma informação adicional) para essa propriedade `Produto`, ou seja, a propriedade está usando o atributo como instrução a mais de comportamento para ele.
	- ![[Pasted image 20240905214410.png]]
		- Se passarmos o mouse em cima do `JsonProperty` vai aparecer isso:
			- *"instrui ao `JsonSerializer` para sempre serializar um membro com o nome especificado"*

Basicamente, um atributo é algo que diz para propriedade ou pra classe que eles irão fazer um comportamento diferente ou que vão representar algo diferente

Podemos atribuir metadados para as classes e propriedades, passando valores ou alterando seu comportamento. Isso é conhecido como:
Metadados


- O processo de _______ consiste em transformar objetos em um fluxo de bytes para seu armazenamento ou transmissão. Estamos falando de:
	- serialização
	
- Uma maneira de armazenar e compartilhar dados estruturados em formato de texto, de forma leve e com uma determinada sintaxe é o formato:
	- json
	
- Podemos compartilhar nosso código como uma solução ou melhoria em comum com outras pessoas, para que elas usem em seus projetos e se beneficie dessa solução, visando o reaproveitamento de código. Quando fazemos isso, estamos montando um(a):
	- pacote (ou biblioteca)
	
- Para instalar um pacote, podemos fazer visualmente ou pela linha de comando no terminal. Pela linha de comando, para instalar um pacote pelo .NET CLI devemos executar o:
	- `dotnet add package nome_do_pacote`
	
- No formato JSON, precisamos representar o início e o fim de um objeto, e esse objeto pode conter outros objetos, bem como também pertencer a uma coleção. Representamos o início e fim de um objeto usando o:
	- {}