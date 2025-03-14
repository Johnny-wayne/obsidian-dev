
### Objetivo Geral

Aprender e desenvolver uma API, utilizando o Entity Framework para persistência de dados em banco de dados relacionais, juntamente com seus principais conceitos e funcionalidades.

---
### O que é uma API?

Uma API (Application Programming Interface) é uma forma de comunicação entre computadores ou programas de computadores.

Em outras palavras, é um software que fornece informações para outro software.

---
### Construindo esta porra

Vamos abrir o VScode bonitão e rodar essa bufunfa:

```C#
dotnet new webapi --framework net6.0
//Porque estão usando a versão 6 no curso
```
Inicialmente, já vai vir junto algo pré-pronto de uma API de Clima.

Aí vamos rodar:
```C#
dotnet watch run
```
[[dotnet watch run]]

Quando executamos, ele abre uma página web que serve como um frontend da API, chamado de Swagger, a API não tem cara nem rosto, quando criamos uma API no .NET nós temos o Swagger que é basicamente a documentação da nossa API.

- Swagger
	![[Pasted image 20241004120945.png]]
	Que é essa telinha bem bonitona
	
	Se abrirmos esse Get aí, clicarmos em Try Out e depois Execute, ele vai fazer uma chamada da API

O Swagger não é obrigatório, ele serve mais pros dev's testarem as API's e como uma forma de documentação.

---
#### Criando a Controller

###### O que é uma Controller

- É uma ***Classe*** que vai agrupar as nossas ***Requisições HTTP*** e vai disponibilizar os seus ***Endpoints*** .

-  **Convenção:** 
	- Ao criar uma classe "Controller", é recomendado utilizar: *`NomeDaClasseController`* 

- Quando criamos uma Controller, podemos ver que é idêntica a uma classe comum, ela apenas carrega alguns atributos a mais.

- Criamos uma nova classe `UsuarioController`:
	```C#
	using Microsoft.AspNetCore.Mvc;
	
	namespace API.Controllers
	{
	    [ApiController]  // Atributo
	    [Route("[controller]")] // Atributo
	    public class UsuarioController : ControllerBase //Herda
	    {
	        [HttpGet("ObterDataHoraAtual")] //Implementa um nome de como podemos chamar o método da API
	        public IActionResult ObterDataHora() // Interface I
	        {
	            var obj = new 
	            {
	                Data = DateTime.Now.ToLongDateString(),
	                Hora = DateTime.Now.ToShortTimeString()
	            };
	
	            return Ok(obj); //método que já vem
	        }
	    }
	}
	```

Aí se rodarmos isso aí e formos lá no Swagger, vamos poder testar nossa controller e ver que irá retornar nosso dados de data e hora atual, (o formato varia).

---
#### Entendendo as rotas

- `'https://localhost:7275/Usuario` - Se refere a Controller (ele sempre ignora a parte "Controller" do nome da Controller)
- `https://localhost:7275/Usuario/ObterDataHoraAtual` - Se refere a essa parte da Controller
	```C#
	[HttpGet("ObterDataHoraAtual")] 
	public IActionResult ObterDataHora()
	```

![[Pasted image 20241008122706.png]]

---
#### Endpoint com parâmetro

*Criamos um novo método/endpoint na classe*
```C#
[HttpGet("Apresentar/{nome}")]
public IActionResult Apresentar(string nome) {
	var mensagem = $"Olá {nome}, seja bem vindo!";
	return Ok(new {mensagem});
}
```

- Endpoint no Swagger
	![[Pasted image 20241008124008.png]]
	- Reposta
		![[Pasted image 20241008124041.png]]

- `https://localhost:7236/Usuario/Apresentar/Bibe` - retorna:
	- `{"mensagem":"Olá Bibe, seja bem vindo!"}`
- *"Bibe"*, age como um parâmetro de URL

Antes da URL ser executada, ela verifica antes se os parâmetros estão preenchidos, ou se existem.

---
#### Criando a classe entidade

*Vamos criar um CRUD de contatos, como se fosse uma agenda, usando o [[EF - Entity Framework]]*

Criamos uma pasta chamada "Entities" para colocarmos as classes referentes ao EF e criamos uma classe chamada `Contato.cs`

```C#
namespace API.Entities
{
    public class Contato
    {
        public int Id { get; set; }
        public string Nome { get; set; }
        public string Telefone { get; set; }
        public bool Ativo { get; set; }
    }
}
```

---

##### Criando o Contexto

Agora vamos criar o ***Contexto***. E que porra é essa?

É uma classe que centraliza todas as nossas informações em determinado banco de dados.

- Criamos uma pasta chamada `Context`
	- Depois uma classe chamada `AgendaContext.cs`

#pesquisar
```C#
using Microsoft.EntityFrameworkCore;
using API.Entities;

namespace API.Context
{
    public class AgendaContext : DbContext
    {
        // aqui vamos passar a nossa conexão com o banco e passar para o DbContext.options
        public AgendaContext(DbContextOptions<AgendaContext> options) : base(options)
        {

        }
        // aqui iremos colocar uma propriedade que refere a nossa entidade, no caso Contato.cs
        public DbSet<Contato> Contatos{ get; set; }
        //tudo que tá como DbSet<> vai virar tabela
    }
}
```

Entidade = Classe no meu programa & tabela no banco de dados

Para entender melhor, vá aqui:
- [[DbSet]] 
- [[DbContextOptions]]

--- 

##### Configurando a conexão

Vamos cadastrar nossa conexão no nosso arquivo de configuração e vamos também inicializar nosso DbContext

Temos dois arquivos Json de configuração:
- `appsettings.Development.json` - Para o ambiente de desenvolvimento
- `appsettings.json` - Para o ambiente de produção

- Dentro da `appsettings.Development.json`:
	```json
	{
	  "Logging": {
	    "LogLevel": {
	      "Default": "Information",
	      "Microsoft.AspNetCore": "Warning"
	    }
	  }
	}
	```

- Vamos adicionar essa parte:
	```json
	{
	  "Logging": {
	    "LogLevel": {
	      "Default": "Information",
	      "Microsoft.AspNetCore": "Warning"
	    }
	  },
	  "ConnectionStrings": {
	    "ConexaoPadrao": "Server=localhost\\sqlexpress; Initial Catalog=Agenda; Integrated Security=True"
	  }
	}
	```
	- `Server=localhost\\sqlexpress;`
		- Conexão com o banco de dados
	- `Initial Catalog=Agenda;`
		- Nome do nosso banco de dados, se não existir o EF cria
	- `Integrated Security=True`
		- Método de autenticação: nesse caso, é o mesmo do Windows

O nome disso é ***==Connection String==*** e o nosso ***Context*** vai usa-la para se conectar com o nosso banco, pra isso a gente precisa dizer pro Context usar ela.

Agora vamos lá pra `Program.cs` e vamos colocar uma configuração adicional lá:

- Inicialmente ele é assim:
	```C#
	var builder = WebApplication.CreateBuilder(args);
	
	// Add services to the container.
	
	builder.Services.AddControllers();
	// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
	builder.Services.AddEndpointsApiExplorer();
	builder.Services.AddSwaggerGen();
	
	var app = builder.Build();
	
	// Configure the HTTP request pipeline.
	if (app.Environment.IsDevelopment())
	{
	    app.UseSwagger();
	    app.UseSwaggerUI();
	}
	
	app.UseHttpsRedirection();
	
	app.UseAuthorization();
	
	app.MapControllers();
	
	app.Run();
	```

- Vamos adicionar essa parte, não precisa ficar exatamente aqui, mas é bom colocar antes:
	```C#
	using API.Context;
	using Microsoft.EntityFrameworkCore;
	
	var builder = WebApplication.CreateBuilder(args);
	
	// Add services to the container.
	builder.Services.AddDbContext<AgendaContext>(Options =>
		Options.UseSqlServer(builder.Configuration.GetConnectionString("ConexaoPadrao")));
	
	```
	Grande pra krl, eu sei. Mas precisamos entender né, então vamo lá:


---

#### Entendendo as migrations

Vamos entender o que são migrations:

Migrations 

Depois que rodarmos:
```C#
dotnet-ef migrations add CriacaoTabelaContato
```

Ele vai criar automaticamente uma pasta chamada 'Migrations' que vai conter 3 arquivos:
![[Pasted image 20241013163711.png]]


Dentro do `_CriacaoTabelContato.cs` (o primeiro), vamo encontrar estes dois métodos:
```C#
	//... E tem mais depois
	
	protected override void Up(MigrationBuilder migrationBuilder)
	{
		migrationBuilder.CreateTable(
			name: "Contatos",
			columns: table => new
			{
				Id = table.Column<int>(type: "int", nullable: false)
					.Annotation("SqlServer:Identity", "1, 1"),
				Nome = table.Column<string>(type: "nvarchar(max)", nullable: true),
				Telefone = table.Column<string>(type: "nvarchar(max)", nullable: true),
				Ativo = table.Column<bool>(type: "bit", nullable: false)
			},
			constraints: table =>
			{
				table.PrimaryKey("PK_Contatos", x => x.Id);
			});
	}
	
	protected override void Down(MigrationBuilder migrationBuilder)
	{
		migrationBuilder.DropTable(
			name: "Contatos");
	}
	
	//... Tem mais antes
```
- `Up()`: Aplicar as mudanças no banco de dados
- `Down()`: Pra fazermos um Rollback

- E da onde saíram essas propriedades? Da nossa classe Contato
	
	`Contato.cs`
	```C#
	public class Contato
	{
		public int Id { get; set; }
		public string Nome { get; set; }
		public string Telefone { get; set; }
		public bool Ativo { get; set; }
	}
	```
	
	Basicamente:
	- Definimos as Entities: Classes que serão representadas como tabelas no DB
	- Depois construímos um Context, definimos a configuração no JSON, depois configuramos ele no `Program.cs`
	- Aí implementamos uma Migrations que transforma as entidades em tabelas
	
	Fun fact:
		Por padrão nomeamos as entities no singular. Neste caso `Contato.cs`, mas a Migration criou uma tabela, chamada `Contatos`, ela faz isso porque sabe que o padrão da criação da classe no C# é no singular, e coloca um S depois automaticamente.

Esse código, não significa que a nossa classe está criada no nosso banco de dados. Precisamos rodar esse comando primeiro:

```C#
dotnet-ef database update
```

- Agora sim está criada a nossa tabela, automaticamente no nosso DB: 
	![[Pasted image 20241013170605.png

---
#### Criando a controller e o endpoint de Create

Vamos inserir os dados com o EF. Como iniciamos a tabela, ela tá fazia, então vamos criar uma Controller e uns endpoints pra colocar algumas coisas nela. 

- Começamos criando uma classe Controller `ContatoController.cs` 

```C#
using API.Context;
using API.Entities;
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class ContatoController : ControllerBase
    {
        private readonly AgendaContext _context;
        public ContatoController(AgendaContext context)
        {
            _context = context;
        }

        [HttpPost]
        public IActionResult Create(Contato contato)
        {
            _context.Add(contato);
            _context.SaveChanges();
            return Ok(contato);
        }
    }
}
```

- No atributo `[HttpPost]` do método `Create()`  não colocamos uma rota como no atributo         `[HttpGet("Apresentar/{nome}")]` de outra Controller, porque só estamos realizando o POST desses dados.

- Com isso criamos um endpoint de uma API que faz um `[HttpPost]` no banco de dados.
	- Dentro do Swagger, é possível preencher manualmente um JSON que realiza o Post direto no banco de dados.
	- Clicamos em "Try Out", tiramos o Id porque não precisamos, e preenchemos o restante dos dados.
	- Clicamos em execute, e pronto

---
#### Criando o endpoint obter por ID

```C#
using API.Context;
using API.Entities;
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class ContatoController : ControllerBase
    {
        private readonly AgendaContext _context;
        public ContatoController(AgendaContext context)
        {
            _context = context;
        }

        [HttpPost]
        public IActionResult Create(Contato contato)
        {
            _context.Add(contato);
            _context.SaveChanges();
            return Ok(contato);
        }

        [HttpGet("{id}")]
        public IActionResult GetById(int id)
        {
            var contato = _context.Contatos.Find(id);

            if (contato == null)
            {
                return NotFound();
            }
            
            return Ok(contato);
        }
    }
}
```

**Endpoint isolado:**
```C#
[HttpGet("{id}")]
public IActionResult GetById(int id)
{
	//Parte mais importante do código
	var contato = _context.Contatos.Find(id);

	//Validação
	if (contato == null)
	{
		return NotFound();
	}
	
	return Ok(contato);
}
```

- Caso não retornemos um `id` válido, ele retorna um `NotFound()`, com `status 404`.

---
#### Criando o endpoint de update

**Como eu pensei que poderia ser:**
```C#
	[HttpPut]
	public IActionResult Update(Contato Contato)
	{
		_context.Contatos.Update(Contato);
	}
```

**Como é:**
```C#
	[HttpPut("{id}")]
	public IActionResult Update(int id, Contato contato) 
	{
		//identificação do Contato para atualizar
		var contatoBanco = _context.Contatos.Find(id);
		
		//Validação básica
		if (contatoBanco == null )
			return NotFound();
		
		//Preenchendo com os dados
		contatoBanco.Nome = contato.Nome;
		contatoBanco.Telefone = contato.Telefone;
		contatoBanco.Ativo = contato.Ativo;
		
		//Atualizando e salvando...
		_context.Update(contatoBanco);
		_context.SaveChanges();
		
		//Ok
		return Ok(contatoBanco);
	}
```
Para o Update, pegamos dois parâmetros:
- Id do Contato no banco do que vamos atualizar
	- `ContatoBanco = Id(no banco de dados)`
- Contato com os dados que estamos usando para atualizar o contato do banco

---
#### Criando o endpoint de delete

**Como pensei que seria:**
```C#
 [HttpDelete("{id}")]
        public IActionResult Delete(int id)
        {
            var contatoBanco = _context.Contatos.Find(id);
			
            if (contatoBanco == null)
                return NotFound();
			
            _context.Contatos.Remove(contatoBanco);
            _context.SaveChanges();
			
            return Ok(contatoBanco);
        }
```

**Como realmente é:**
```C#
public IActionResult Delete(int id)
{
	var contatoBanco = _context.Contatos.Find(id);
	
	if (contatoBanco == null)
		return NotFound();
	
	_context.Contatos.Remove(contatoBanco);
	_context.SaveChanges();
	
	//é um retorno de sucesso, mas não tem o que retornar, então retorna nada 
	return NoContent();
}
```

Aqui vai retornar um código 204 que é "Retornei sucesso, mas não te retornei nada".

A família 200 é para ==sucesso==

Agora, se dermos um GET, no mesmo id, vai dar 404

---
#### Criando o endpoint de obter por nome

**Como eu pensei que seria:**
```C#
[HttpGet("{name}")]
public IActionResult GetByName(int name)
{
	var contato = _context.Contatos.Find(name);

	if (contato == null)
	{
		return NotFound();
	}

	return Ok(contato);
}
```

**Como realmente é:**
```C#
[HttpGet("name")]
public IActionResult GetByName(string name)
{
	var contatos = _context.Contatos.Where(x => x.Nome.Contains(name));
	return Ok(contatos);
}
```
*Ele retorna uma lista em JSON*

> Obs: Se tiver Eduardo e Buta no nosso banco, e fizermos um GET com parâmetro "u", ele irá retornar os dois, porque os dois têm "u".


- Pontos importantes para aprender: #pesquisar 
	- O porquê:
		- `[HttpGet("{name}")]` dá errado
		- E `[HttpGet("name")]` não
	- Entender a sintaxe e o funcionamento do:
		- `_context.Contatos.Where(x => x.Nome.Contains(name));`
	

---
#### Verbos HTTP

![[Pasted image 20241016000105.png]]

- Patch - atualizar só uma parte
- Put - tudo

--- 
#### Recapitulando a construção da nossa API

Instalamos a nossa ferramenta **Entity Framework** (a nível de máquina), e também dois pacotes: 
- `Microsoft.EntityFrameworkCore.SqlServer - version 6.0.5`
- `Microsoft.EntityFrameworkCore.Design - version 6.0.5`

- `Controllers/ContatoController.cs` 
	- Basicamente, a API em si, com os endpoints e verbos HTTP
- `appsettings.Development.json`
	- Onde configuraremos a nossa connection string. Mais ou menos nesse formato:
		```json
		{
		  "Logging": {
		    "LogLevel": {
		      "Default": "Information",
		      "Microsoft.AspNetCore": "Warning"
		    }
		  },
		  "ConnectionStrings": {
		    "ConexaoPadrao": "Server=localhost\\sqlexpress; Initial Catalog=Agenda; Integrated Security=True"
		  }
		}

		```
		A chave `"ConnectionStrings"` precisa ter esse nome mesmo, mas a `"ConexaoPadrao"` pode ter outro nome.
- `Entities/Contato.cs`
	- Arquivo/entidade que age como classe para nossa API e como tabela no nosso banco de dados.
- `Context/AgendaContext.cs`
	- É a nossa classe que vai acessar nosso banco de dados, aqui é onde chamaremos a conexão com nosso banco. Por isso precisa ter um construtor nesse formato:
		- `public AgendaContext(DbContextOptions<AgendaContext> options) : base(options)`
- `Program.cs`
	- Nesse caso, só usamos pra configurar a conexão com o DB passando qual banco de dados estamos usando (nesse caso SqlServer), e a connection string.
- `Migrations/(vários)`
	- Código para poder espelhar as alterações do código no DB.
	- Obs: Se não aplicarmos a migration, não acontece nada.

---
#### Alterando o endpoint Create

**Como era:**
```C#
[HttpPost]
public IActionResult Create(Contato contato)
{
	_context.Add(contato);
	_context.SaveChanges();
	return Ok(contato);
}
```

**Como deixamos:**
```C#
[HttpPost]
public IActionResult Create(Contato contato)
{
	_context.Add(contato);
	_context.SaveChanges();
	return CreatedAtAction(nameof(GetById), new { id = contato.Id }, contato);
}
```

- `CreatedAtAction(nameof(GetById), new { id = contato.Id }, contato);`
	- Após criar, para obtermos o registro recém criado, podemos chamar o obter por id (`GetById`), estamos retornando o id recém criado e a própria informação do Contato.

E aí quando rodarmos com o `dotnet watch run`, vamos preencher lá no Swagger e vai retornar isso:
![[Pasted image 20241016221840.png]]

Agora ele vai nos retornar, algo chamado ***Location***. Ou seja, o `CreatedAtAction` vai criar o recurso pra você, e vai falar: "Criei pá tu, pra tu acessar, é nesse endereço".

Ou seja, além do ***Response Body*** do Json, que retorna `id: 5` e outras coisas ali em cima, eu posso ter minha minha ***location*** URL/5 que foi recém criada