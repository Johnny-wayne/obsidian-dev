___ 
#### Estrutura inicial

Criaremos um projeto web no dotnet
```
dotnet new web -o minimal-api
```

Aí ele vai criar nossa aplicação a partir de um boilerplate (um template inicial pra que a gente consiga codar com mais facilidade)

Se entrarmos com `cd` na pasta que criamos do `minimal-api` e depois digitarmos `code .` ele abre o VScode automaticamente na pasta que criamos.

Esse boilerplate tem uma pasta chamada *Properties* que possui dados como as portas que ele starta a aplicação na nossa máquina e na de outros computadores também

Nosso `program.cs` inicialmente fica assim:
```C#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Hello World!");

app.Run();
```

É muito parecido com o Express do Node.js.

A ideia do minimal API não é ser robusta.


---
#### Arquitetura

![[Pasted image 20241031193833.png]]

---
#### Começando a criar
*Criando uma rota de login para a validação em memória*

`Program.cs`
```C#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Hello World!");

app.MapPost("/login", (LoginDTO loginDTO) => {
    if(loginDTO.Email == "adm@teste.com" && loginDTO.Senha == "123456") {
        return Results.Ok("Login com sucesso");
    }
    else 
        return Results.Unauthorized();
});

app.Run();

public class LoginDTO
{
    public string Email { get; set; } = default!;
    public string Senha { get; set; } = default!;
}
```

- Criamos um `MapPost()` que recebe como parâmetro `loginDTO` e faz uma validação de login/usuário.
	- **DTO** - *Data Transfer Object*

- Podemos definir classes no próprio `Program.cs`, mas é importante que defini-las abaixo do `app.Run()`;

Se você for ver direito, tem coisas bem parecidas (praticamente iguais) com as da web-api

Agora a gente vai colocar um breakpoint nessa linha:
```C#
    if(loginDTO.Email == "adm@teste.com" && loginDTO.Senha == "123456") {
```

Vai abrir o ***Postman*** e fazer uma requisição POST para `https://localhost:7223/login` no ***body*** vamos no tipo ***raw*** e no formato ***JSON***. 

*(você se acha lá dentro...)*
	*foi oq ela disse*

E lá dentro, você vai escrever:
```json
{
    "email": "adm@teste.com",
    "senha": "123456"
}
```

E teoricamente, vai retornar: `"Login com sucesso"`

Se você colocar uma senha invalida ou usuário invalido 

---
#### Mexendo com o DB
Configurando o projeto com Entity Framework e tabela de administradores

##### Estrutura inicial

- Aqui vamos baixar os pacotes:
	- `dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 8.0.10`
	- `dotnet add package Pomelo.EntityFrameworkCore.MySql --version 8.0.2`

- Ele vai misturar duas arquiteturas:
	- Clean architecture
	- Onion architecture

- A estrutura inicial vai ser assim:
	![[Pasted image 20241102183903.png]]


Ele preencheu com `.gitkeep` as pastas vazias que queria que o git/Github reconhecesse.
- E também refatorou esse trecho de código:
	```C#
	namespace MinimalApi.DTOs;
	
	public class LoginDTO
	{
	    public string Email { get; set; } = default!;
	    public string Senha { get; set; } = default!;
	}
	```
	Para dentro da pasta `DTOs` e nomeamos o arquivo de `LoginDTO.cs`

adicionamos um `.gitignore`, fomos para `git ignore io`, e preenchemos a barrinha lá com: `Windows, macOS, Linux, DotnetCore, VisualStudioCode`, depois apertamos me criar.

Aí subimos pro Github.

##### Produzindo

1. Dentro da pasta `Db` ele cria o `DbContext` chamado `DbContexto`.

2. Depois cria uma entidade chamada `Administrador.cs`
	```C#
	namespace minimal_api.Dominio.Entidades
	{
	    public class Administrador
	    {
	        public int Id { get; set; } = default!;
			
	        public string Email { get; set; } = default!;
			
	        public string Senha { get; set; } = default!;
	        
	        public string Perfil { get; set; } = default!;
	    }
	}
	```

3. Agora, dentro do `DbContexto`:
	```C#
	namespace MinimalApi.Infraestrutura.Db;
	
	public class DbContexto : DbContext
	{	
		//adiciona a entidade como DbSet<Administradores>
		public DbSet<Administrador> Administradores { get; set; } = default!;
		
		//basicamente configura pra usar MySql e reserva a string de conexão
		protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
		{
			optionsBuilder.UseMySql(
				"string de conexão", 
				ServerVersion.AutoDetect("string de conexão")
			);
		}
	}
	```

4. Antes de gerar o *migration* nós vamos colocar alguns atributos na nossa entidade
	```C#
	namespace minimal_api.Dominio.Entidades
	{
	    public class Administrador
	    {
	        [Key]
	        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
	        public int Id { get; set; } = default!;
	
	        [Required]
	        [StringLength(255)]
	        public int Email { get; set; } = default!;
	
	        [StringLength(50)]
	        public int Senha { get; set; } = default!;
	        
	        [StringLength(10)]
	        public int Perfil { get; set; } = default!;
	    }
	}
	```
	- `[Key]` - identifica a propriedade como uma key do Db
	- `[DatabaseGenerated(DatabaseGeneratedOption.Identity)]` - permite o autoincrement da key
	- `[Required]` - exige que o campo seja preenchido
	- `[stringLength(number)]` - acho que é bem autoexplicativo

5. Para continuarmos, precisaremos também adicionarmos nossa string de conexão dentro do nosso `appsettings.json`
	```json
	{
	  "Logging": {
	    "LogLevel": {
	      "Default": "Information",
	      "Microsoft.AspNetCore": "Warning"
	    }
	  },
	  "AllowedHosts": "*",
	  "ConnectionStrings": {
	    "mysql": "Server=localhost; Database=minimal_api; Uid=root; Pwd=root"
	  }
	}
	```
	Ele procurou um "Template" de connection strings do mysql em um site, depois colou e preencheu.

6. Agora, para pudermos pegar nossa string de conexão, precisaremos implementar um construtor no nosso Context.
	```C#
	public class DbContexto : DbContext
	{
	    private readonly IConfiguration _configuracaoAppSettings;

		//configuraçãoAppSettings vai ser a string de conexão que receberemos do nosso appsettings.json
	    public DbContexto(IConfiguration configuracaoAppSettings)
	    {
	        _configuracaoAppSettings = configuracaoAppSettings;
	    }
	    
	    public DbSet<Administrador> Administradores { get; set; } = default!;
	
	    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
	    {
		    //Esse "mysql" foi definido no nosso appsettings.json
		    var stringConexao = _configuracaoAppSettings.GetConnectionString("mysql")?.ToString();
			
			//Se a string de conexão não for null ou empty...
	        if(!string.IsNullOrEmpty(stringConexao))
	        {
	            optionsBuilder.UseMySql(
	               stringConexao, 
	                ServerVersion.AutoDetect(stringConexao)
	            );  
	        }
	    }
	}
	```

7. Aí vamos precisar chamar o construtor lá no nosso `Program.cs`
	```C#
	using MinimalApi.Infraestrutura.Db;
	using MinimalApi.DTOs;
	using Microsoft.EntityFrameworkCore;
	
	var builder = WebApplication.CreateBuilder(args);
	
	builder.Services.AddDbContext<DbContexto>(options => {
	    options.UseMySql(
	        builder.Configuration.GetConnectionString("mysql"),
	        ServerVersion.AutoDetect(builder.Configuration.GetConnectionString("mysql"))
	    );
	});
	
	var app = builder.Build();
	
	app.MapGet("/", () => "Hello World!");
	
	app.MapPost("/login", (LoginDTO loginDTO) => {
	    if(loginDTO.Email == "adm@teste.com" && loginDTO.Senha == "123456") {
	        return Results.Ok("Login com sucesso");
	    }
	    else 
	        return Results.Unauthorized();
	});
	
	app.Run();
	```
	Honestamente, não entendi muita coisa, mas parece ser bem parecido com o outro CRUD que fizemos.

8. `DbContexto`:
	```C#
	protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
	    //Adicionamso essa validação aqui
        if(!optionsBuilder.IsConfigured)
        {
            var stringConexao = _configuracaoAppSettings.GetConnectionString("mysql")?.ToString();
            if(!string.IsNullOrEmpty(stringConexao))
            {
                optionsBuilder.UseMySql(
                stringConexao, 
                    ServerVersion.AutoDetect(stringConexao)
                );  
            }
        }
    }
	```
	Validação desgraçada, eu esqueci da porra da exclamação e perdi uns 30 ou 40 minutos procurando a porra do erro, vsfd.

9. Agora geraremos nossa migrations:
	`dotnet ef migrations add AdministradorMigration` e depois `dotnet ef database update`

Se for acessar o MySQL pelo terminal, acessa pelo shell dele que tá instalado, pelo VScode não consegui.

---
#### Criando Seed para cadastrar administrador padrão

Agora nosso próximo passo, é validar nosso usuário (administrador) no banco de dados. Pra isso, precisamos cadastrar um usuário no banco de dados, pra validar ele depois.

- E pra isso, vamos criar um ***Seed*** no nosso `DbContexto`:
	```C#
	public class DbContexto : DbContext
	{
	    private readonly IConfiguration _configuracaoAppSettings;
	    
	    public DbContexto(IConfiguration configuracaoAppSettings)
	    {
	        _configuracaoAppSettings = configuracaoAppSettings;
	    }
	    
	    public DbSet<Administrador> Administradores { get; set; } = default!;
		
		//Seed
	    protected override void OnModelCreating(ModelBuilder modelBuilder)
	    {
	        modelBuilder.Entity<Administrador>().HasData(
	            new Administrador { 
	                Id = 1,
	                Email = "Administrador@teste.com",
	                Senha = "123456",
	                Perfil = "Adm"
	            }
	        );    
	    }
	    
	    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
	    {
	        if(!optionsBuilder.IsConfigured)
	        {
	            var stringConexao = _configuracaoAppSettings.GetConnectionString("mysql")?.ToString();
	            if(!string.IsNullOrEmpty(stringConexao))
	            {
	                optionsBuilder.UseMySql(
	                stringConexao, 
	                    ServerVersion.AutoDetect(stringConexao)
	                );  
	            }
	        }
	    }
	}
	```
	- `Seed` - Uma função para podermos cadastrar esse administrador inicial

- Seed:
	```C#
	//Seed
	protected override void OnModelCreating(ModelBuilder modelBuilder)
	{
		modelBuilder.Entity<Administrador>().HasData(
			new Administrador { 
				Id = 1,
				Email = "Administrador@teste.com",
				Senha = "123456",
				Perfil = "Adm"
			}
		);    
	}
	```

Depois:
- `dotnet ef migrations add SeedAdministrador`
- `dotnet ef database update`

---
#### Validando administrador com login e senha no banco de dados

1. Vamos criar uma classe de serviço
	`Dominio/Servicos/AdministradorServico.cs`
	```C#
	using minimalApi.Dominio.Entidades;
	using minimalApi.Dominio.Interfaces;
	using MinimalApi.DTOs;
	using MinimalApi.Infraestrutura.Db;
	
	
	namespace MinimalApi.Dominio.Servicos;
	
	public class AdministradorServico : IAdministradorServico
	{
	    private readonly DbContexto _contexto;
	    
	    public AdministradorServico(DbContexto contexto)
	    {
	        _contexto = contexto;
	    }
	    
	    public Administrador? Login(LoginDTO loginDTO)
	    {
	        var adm = _contexto.Administradores.Where(a => a.Email == loginDTO.Email && a.Senha == loginDTO.Senha).FirstOrDefault();
	        return adm;
	    }
	}
	```
	Mas antes de criarmos os métodos desse serviço, precisamos criar interfaces para que futuramente possamos realizar ***Mocks*** lá em nossos testes.

2. Criando a interface:
	`Dominio/Interfaces/iAdministradorServico`
	```C#
	using minimal_api.Dominio.Entidades;
	using MinimalApi.DTOs;
	
	namespace minimal_api.Dominio.Interfaces
	{
	    public interface IAdministradorServicos
	    {
	        Administrador? Login(LoginDTO loginDTO);
	    }
	}
	```

3. Implementando a interface:
	```C#
	using minimalApi.Dominio.Entidades;
	using minimalApi.Dominio.Interfaces;
	using MinimalApi.DTOs;
	using MinimalApi.Infraestrutura.Db;
	
	namespace MinimalApi.Dominio.Servicos;
	
	public class AdministradorServico : IAdministradorServico
	{
	    private readonly DbContexto _contexto;
	    public AdministradorServico(DbContexto contexto)
	    {
	        _contexto = contexto;
	    }
	    public Administrador? Login(LoginDTO loginDTO)
	    {
	        var adm = _contexto.Administradores.Where(a => a.Email == loginDTO.Email && a.Senha == loginDTO.Senha).FirstOrDefault();
	        return adm;
	    }
	}
	```
	- `FirtsOrDefault()` - Retorna alguma coisa, ou nulo.

4. Usando no `Program.cs`
	```C#
	using MinimalApi.Infraestrutura.Db;
	using MinimalApi.DTOs;
	using Microsoft.EntityFrameworkCore;
	using minimalApi.Dominio.Interfaces;
	using MinimalApi.Dominio.Servicos;
	using Microsoft.AspNetCore.Mvc;
	
	var builder = WebApplication.CreateBuilder(args);
	
	builder.Services.AddScoped<IAdministradorServico, AdministradorServico>();
	
	builder.Services.AddDbContext<DbContexto>(options => {
	    options.UseMySql(
	        builder.Configuration.GetConnectionString("mysql"),
	        ServerVersion.AutoDetect(builder.Configuration.GetConnectionString("mysql"))
	    );
	});
	
	var app = builder.Build();
	
	app.MapGet("/", () => "Hello World!");
	
	app.MapPost("/login", ([FromBody] LoginDTO loginDTO, IAdministradorServico administradorServico) => {
	    if(administradorServico.Login(loginDTO) != null) {
	        return Results.Ok("Login com sucesso");
	    }
	    else 
	        return Results.Unauthorized();
	});
	
	app.Run();
	
	
	```
	Honestamente, não entendi porra nenhuma nessa parte. #pesquisar #importante 

5. Testando
	1. Agora, damos um `dotnet watch run`, esperamos abrir o `localhost` no nosso browser, depois pegamos a port que nos indicar. 
	2. Abrimos o **Postman** colocamos a Url, nesse caso: `https://localhost:5122/login`
	3. Vamos no body, e vamos testar primeiro com o valor errado:
		```json
		{
		    "email": "adm@teste.com",
		    "senha": "123456"
		}
		//Retorna 401
		```
	4. Agora vamos testar com o valor certo:
		```json
		{
		    "email": "Administrador@teste.com",
		    "senha": "123456"
		}
		//Retorna "Login com sucesso"
		```
		==Plmds, lembre-se de colocar http em vez de https==

---
#### Configurando modelo de veículos


- Adicionamos uma entidade chamada `veiculo.cs`
	```C#
	using System.ComponentModel.DataAnnotations;
	using System.ComponentModel.DataAnnotations.Schema;
	
	namespace minimalApi.Dominio.Entidades
	{
	    public class Veiculo
	    {
	        [Key][DatabaseGenerated(DatabaseGeneratedOption.Identity)]
	        public int Id { get; set; } = default!;
	
	        [Required]
	        [StringLength(150)]
	        public string Nome { get; set; } = default!;
	
	        [Required]
	        [StringLength(100)]
	        public string Marca { get; set; } = default!;
	
	        [Required]
	        public int Ano { get; set; } = default!;
	    }
	}
	```

Também adicionamos `[Required]` nas propriedades da classe `Administrador.cs`

- Fazemos um mapeamento no `DbContext` adicionando um `DbSet` no Context também
	```C#
	 public DbSet<Administrador> Administradores { get; set; } = default!;
	
	    public DbSet<Veiculo> Veiculos { get; set; } = default!;
	```

- Nosso próximo passo, é fazer a nossa migrations:
	- `dotnet ef migrations add VeiculosMigration`
	- `dotnet ef database update`
	- `desc veiculos;` -> no mysql shell

- Em seguida, criamos um Serviço e uma Interface para esta entidade.
	  note que serviços estão sendo usados, de forma análoga às controllers do módulo: [[Introdução as API's com C-sharp]]

- `Dominio/Interfaces/IVeiculoServico.cs`
	```C#
	using minimalApi.Dominio.Entidades;
	using MinimalApi.DTOs;
	
	namespace minimalApi.Dominio.Interfaces
	{
	    public interface IVeiculoServico
	    {
	        List<Veiculo> Todos(int? pagina = 1, string? nome = null, string? marca=null);
	        Veiculo? BuscaPorId(int id);
	        void Incluir(Veiculo veiculo);
	        void Atualizar(Veiculo veiculo);
	        void Apagar(Veiculo veiculo);
	    }
	}
	```
- `Dominio/Servicos/VeiculoServico.cs`
	```C#
	using minimalApi.Dominio.Entidades;
	using minimalApi.Dominio.Interfaces;
	using MinimalApi.DTOs;
	using MinimalApi.Infraestrutura.Db;
	
	namespace MinimalApi.Dominio.Servicos;
	
	public class VeiculoServico : IVeiculoServico
	{
	    private readonly DbContexto _contexto;
	    public VeiculoServico(DbContexto contexto)
	    {
	        _contexto = contexto;
	    }
		
	    public void Apagar(Veiculo veiculo)
	    {
	        _contexto.Veiculos.Remove(veiculo);
	        _contexto.SaveChanges();
	    }
		
	    public void Atualizar(Veiculo veiculo)
	    {
	        _contexto.Veiculos.Update(veiculo);
	        _contexto.SaveChanges();
	    }
		
	    public Veiculo? BuscaPorId(int id)
	    {
	        return _contexto.Veiculos.Where(v => v.Id == id).FirstOrDefault();
	    }
		
	    public void Incluir(Veiculo veiculo)
	    {
	        _contexto.Veiculos.Add(veiculo);
	        _contexto.SaveChanges();
	    }
		
	    public List<Veiculo> Todos(int? pagina = 1, string? nome = null, string? marca = null)
	    {
	        var query = _contexto.Veiculos.AsQueryable();
	        if(!string.IsNullOrEmpty(nome))
	        {
	            // query = query.Where(v => EF.Functions.Like(v.Nome.ToLower(), $"%{nome}%" )
	            query = query.Where(v => v.Nome.ToLower().Contains(nome) == true);
	        }
	
	        int itensPorPagina = 10;
	
	        query = query.Skip((pagina - 1) * itensPorPagina).Take(itensPorPagina);
	
	        return query.ToList();
	    }
	}
	```
	- Esse conceito de paginação dentro do método `Todos()` eu ainda não entendo, mas pelo que pesquisei, tem a ver com dividir os dados em "páginas", pra que eles sejam processados em partes, pq às vezes, tem demais.
		- #pesquisar 

---
#### Configurando o Swagger na aplicação
#importante #pesquisar  A partir de agora, vai ser meio que no fds

Baixamos o Swagger: `dotnet add package Swashbuckle.AspNetCore --version 6.9.0`

- Implementamos outro builder no `Program.cs`:
	```C#
	using MinimalApi.Infraestrutura.Db;
	using MinimalApi.DTOs;
	using Microsoft.EntityFrameworkCore;
	using minimalApi.Dominio.Interfaces;
	using MinimalApi.Dominio.Servicos;
	using Microsoft.AspNetCore.Mvc;
	
	var builder = WebApplication.CreateBuilder(args);
	
	builder.Services.AddScoped<IAdministradorServico, AdministradorServico>();
	
	builder.Services.AddEndpointsApiExplorer(); // Linha adicionada
	builder.Services.AddSwaggerGen(); // Linha adicionada
	
	builder.Services.AddDbContext<DbContexto>(options => {
	    options.UseMySql(
	        builder.Configuration.GetConnectionString("mysql"),
	        ServerVersion.AutoDetect(builder.Configuration.GetConnectionString("mysql"))
	    );
	});
	
	var app = builder.Build();
	
	
	app.MapGet("/", () => "Hello World!");
	
	app.MapPost("/login", ([FromBody] LoginDTO loginDTO, IAdministradorServico administradorServico) => {
	    if(administradorServico.Login(loginDTO) != null) {
	        return Results.Ok("Login com sucesso");
	    }
	    else 
	        return Results.Unauthorized();
	});
	
	app.UseSwagger(); // Linha adicionada
	app.UseSwaggerUI(); // Linha adicionada
	
	app.Run();
	```

Aí é só ir pra: `http://localhost:5122/swagger/index.html`

---
#### Criando a rota Home respondendo por JSON

Vamos configurar nossa home, para que ela atue em um formato diferente

Então vamos criar uma pasta chamada `ModelViews` dentro da pasta `Dominio`. 
E dentro dela, criamos um arquivo chamado:

- `Home.cs`
	```C#
	namespace MinimalApi.Dominio.ModelViews;
	
	public struct Home 
	{
	    public string Mensagem { get => "Bem vindo a API de veículos - Minimal API"; }
	
	    public string Doc { get => "/swagger"; }
	}
	```
Note que ele colocou como `struct`

---
#### CRUD veículos

##### POST para criar veículo

Ele separou o `Program.cs` em `region`'s

- E criou um Post pra veículos
	```C#
	#region Veiculos
    app.MapPost("/veiculos", ([FromBody] VeiculoDTO veiculoDTO, IVeiculoServico veiculoServico) => {
    
    var veiculo = new Veiculo {
        Nome = veiculoDTO.Nome,
        Marca = veiculoDTO.Marca,
        Ano = veiculoDTO.Ano
    };
    veiculoServico.Incluir(veiculo);

	//Se não me engano esse Created() pede uma URL e/ou um objeto
    return Results.Created($"/Veiculo/{veiculo.Id}", veiculo);
});
	```
- Criou também um `VeiculoDTO`:
	```C#
	namespace MinimalApi.DTOs;
	
	public record VeiculoDTO 
	{
	    public string Nome { get; set; } = default!;
	
	    public string Marca { get; set; } = default!;
	
	    public int Ano { get; set; } = default!;
	}
	```
	Por ser algo mais simples, instanciamos como um `record`, que é uma instância menor que uma classe.
	Também tiramos os atributos `[Required]` e de Length

E por último, para que não dê erro, ele colocou no Builder:
```C#
#region Builder
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddScoped<IAdministradorServico, AdministradorServico>();
builder.Services.AddScoped<IVeiculoServico, VeiculoServico>(); // <----
//... mais código
```

---
##### GET para retornar os veículos

`Program.cs`
```C#
	//O POST fica logo acima
	
	//Esse [FromQuery] parece ser um atributo do parâmetro pagina
	//#pesquisar
	app.MapGet("/veiculos", ([FromQuery] int? pagina, IVeiculoServico veiculoServico) => {
        var veiculos = veiculoServico.Todos(pagina);
	    
        return Results.Ok(veiculos);
    });
```

---
#### Organizando rotas por contexto/escopo no Swagger

Basicamente, ele coloca uma *Tag* no final de cada rota de enpoint:
```C#
//WithTags("Home");
app.MapGet("/", () => Results.Json(new Home())).WithTags("Home");
```

Todo endpoint, ele coloca isso. Pra ficar assim: 
	![[Pasted image 20241107153142.png]]

---
#### GET para retornar um veículo

Meu jeito: ***(funciona)***
```C#
	//parece que o parâmetro [FromQuery] é quando só vc no swagger
	//talvez esteja errado, pq os outros tb são assim...
	app.MapGet("/veiculo", ([FromQuery] int id, IVeiculoServico veiculoServico) => {
        var veiculo = veiculoServico.BuscaPorId(id);
    
        return Results.Ok(veiculo);
    }).WithTags("Veiculos");
```

Jeito do cara:
```C#
	//e o parâmetro [FromRoute] é quando vc pega da rota
	app.MapGet("/veiculos/{id}", ([FromRoute] int id, IVeiculoServico veiculoServico) => {
        var veiculo = veiculoServico.BuscaPorId(id);
	    
        if(veiculo == null) return Results.NotFound();
		
        return Results.Ok(veiculo);
    }).WithTags("Veiculos");
```

---
#### PUT para atualizar veículo

```C#
	app.MapPut("/veiculos/{id}", ([FromRoute] int id, VeiculoDTO veiculoDTO, IVeiculoServico veiculoServico) => {
        var veiculo = veiculoServico.BuscaPorId(id);
        if(veiculo == null) return Results.NotFound();
		
        veiculo.Nome = veiculoDTO.Nome;
        veiculo.Marca = veiculoDTO.Marca;
        veiculo.Ano = veiculoDTO.Ano;
		
        veiculoServico.Atualizar(veiculo);
		
        return Results.Ok(veiculo);
    }).WithTags("Veiculos");
```

---

#### DELETE para apagar veículo

```C#
	app.MapDelete("/veiculos/{id}", ([FromRoute] int id, IVeiculoServico veiculoServico) => {
        var veiculo = veiculoServico.BuscaPorId(id);
        if(veiculo == null) return Results.NotFound();
		
        veiculoServico.Apagar(veiculo);
		
        return Results.NoContent();
    }).WithTags("Veiculos");
```

---
#### Criando validação ao cadastrar e atualizar veículo

A gente vai fazer, com que quando dê merda, possamos retornar uma mensagem customizada.

Pra isso, a gente vai criar um arquivo dentro de `ModelViews`:

```C#
namespace MinimalApi.Dominio.ModelViews;

public struct ErrosDeValidacao 
{
    public List<string> Mensagens { get; set; }
}
```

Depois criaremos uma função dentro do nosso `Program.cs`
```C#
	ErrosDeValidacao validaDTO(VeiculoDTO veiculoDTO)
	{
		var validacao = new ErrosDeValidacao{
			Mensagens = new List<string>()
		};
		
		if(string.IsNullOrEmpty(veiculoDTO.Nome))
			validacao.Mensagens.Add("O nome não pode ser vazio");
		if(string.IsNullOrEmpty(veiculoDTO.Marca))
			validacao.Mensagens.Add("A marca não pode ficar vazia");
		if(veiculoDTO.Ano < 1950)
			validacao.Mensagens.Add("Veículo muito antigo, coloque acima de 1949");
		
		return validacao;
	} 
	```

E depois aplicamos aos endpoints:
```C#
	app.MapPost("/veiculos", ([FromBody] VeiculoDTO veiculoDTO, IVeiculoServico veiculoServico) => {
    
        var validacao = validaDTO(veiculoDTO);
        if(validacao.Mensagens.Count > 0)
            return Results.BadRequest(validacao);

        var veiculo = new Veiculo {
            Nome = veiculoDTO.Nome,
            Marca = veiculoDTO.Marca,
            Ano = veiculoDTO.Ano
        };
        veiculoServico.Incluir(veiculo);

        return Results.Created($"/Veiculo/{veiculo.Id}", veiculo);
    }).WithTags("Veiculos");
    ```

---
#### Criando endpoints para o administrador

A gente vai basicamente fazer o CRUD do Adm agora.

Pra isso, ele criou um DTO:
`AdministradorDTO.cs`
```C#
using MinimalApi.Dominio.Enuns;

namespace MinimalApi.DTOs;
public record AdministradorDTO 
{
    public string Email { get; set; } = default!;
	
    public string Senha { get; set; } = default!;
	//Aqui esse tipo Perfil é um Enun
    public Perfil Perfil { get; set; } = default!;
}
```

Ele também criou uma pasta pra guardar `Enuns` e fez um pra implementar como tipo da propriedade Perfil ali.

`Enuns/Perfil.cs`
```C#
namespace MinimalApi.Dominio.Enuns;

public enum Perfil
{
    Adm,
    editor
}
```

```C#
#region Administradores
app.MapPost("/administradores/login", ([FromBody] LoginDTO loginDTO, IAdministradorServico administradorServico) => {
    if(administradorServico.Login(loginDTO) != null) {
        return Results.Ok("Login com sucesso");
    }
    else 
        return Results.Unauthorized();
}).WithTags("Administradores");

//Postar só um
app.MapPost("/administradores", ([FromBody] AdministradorDTO AdministradorDTO, IAdministradorServico administradorServico) => {

    var validacao = new ErrosDeValidacao{
        Mensagens = new List<string>()
    };

    if(string.IsNullOrEmpty(AdministradorDTO.Email))
        validacao.Mensagens.Add("Email não pode ser vazio");
    if(string.IsNullOrEmpty(AdministradorDTO.Senha))
        validacao.Mensagens.Add("Senha não pode ser vazio");
    if(AdministradorDTO.Perfil == null)
        validacao.Mensagens.Add("Perfil não pode ser vazio");

    if(validacao.Mensagens.Count > 0)
        return Results.BadRequest(validacao);
    
    var administrador = new Administrador {
        Email = AdministradorDTO.Email,
        Senha = AdministradorDTO.Senha,
        Perfil = AdministradorDTO.Perfil.ToString() ?? Perfil.editor.ToString()
    };
    administradorServico.Incluir(administrador);

    return Results.Created($"/ad/{administrador.Id}", administrador);
}).WithTags("Administradores");

//pegar todos
app.MapGet("/administradores", ([FromQuery] int? pagina, IAdministradorServico administradorServico) => {
    return Results.Ok(administradorServico.Todos(pagina));
}).WithTags("Administradores");

//pegar só um
app.MapGet("/administradores/{id}", ([FromRoute] int id, IAdministradorServico administradorServico) => {
    var administrador = administradorServico.BuscaPorId(id);

    if(administrador == null) return Results.NotFound();

    return Results.Ok(administrador);
}).WithTags("Administradores");

#endregion
```

Funciona tudo bonitinho. Mas... aparece a senha quando fazemos o get, e isso é ruim.

##### Escondendo a senha

Por isso, vamos criar um ***ModelView*** e usar ele nos endpoints do CRUD de administrador, retirando a senha no processo.

## deu ruim
*A partir daqui não sei o que aconteceu, mas a conexão falhou e não quis voltar nem fodendo. Então escolhi continuar o curso só anotando o que acontece e depois fazer um clone do projeto.*

Se quiser, tenta refazer algo parecido futuramente.


### Retomando depois da cagada

#### Configurando token JWT no projeto

Antes de mais nada, a gente tem que colocar o pacote do token JWT:
`dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer `

Depois a gente inclui algumas configurações dentro do `appsettings.json`
```json
 "Jwt": "minimal-api-alunos-vamos_lá"
```

Implementa o builder dele:
```C#
builder.Services.AddAuthentication(option => {
    option.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
    option.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
}).AddJwtBearer(option => {
    option.TokenValidationParameters = new TokenValidationParameters
    {
        ValidateLifetime = true,
        IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(key)),
        ValidateIssuer = false,
        ValidateAudience = false
    };
});

builder.Services.AddAuthorization();
```

Pega a key do Jwt no `appsettings.json`
```C#
var key = builder.Configuration.GetSection("Jwt").ToString();
if(string.IsNullOrEmpty(key)) key = "123456";
```

Depois na `#region App` precisamos chamar alguns métodos:
```C#
//A ordem importa
app.UseAuthentication();
app.UseAuthorization();
```

Aí pra indicar qual rota necessita de autorização nós colocamos no finalzinho ali, um `RequireAuthorization()`
```C#
app.MapGet("/administradores", ([FromQuery] int? pagina, IAdministradorServico administradorServico) => {
    var adms = new List<AdministradorModelView>();
    var administradores = administradorServico.Todos(pagina);
    foreach(var adm in administradores)
    {
        adms.Add(new AdministradorModelView{
            Id = adm.Id,
            Email = adm.Email,
            Perfil = adm.Perfil
        });
    }
    Results.Ok(adms);

}).RequireAuthorization().WithTags("Administradores");
//Nessa última linha aqui
```
Naturalmente, ele vai retornar pedindo pra passar o token.

Logo, vamos colocar um `RequireAuthorization()` em todos, menos no Login de Administradores e na Home.

Agora, na hora de fazermos o Login, precisamos ter nele a possibilidade de retornar um token.

Então lá no topo da `#region Administradores`:
```C#
string GerarTokenJWt(Administrador administrador){
    if(string.IsNullOrEmpty(key)) return string.Empty;

    var securityKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(key)); 
    var credentials = new SigningCredentials(securityKey, SecurityAlgorithms.HmacSha256);

    var claims = new List<Claim>()
    {
        new Claim("Email", administrador.Email),
        new Claim("Perfil", administrador.Perfil)
    };

    var token = new JwtSecurityToken(
        claims: claims,
        //Aqui mostra que o token expira depois de 1 dia
        expires: DateTime.Now.AddDays(1),
        signingCredentials: credentials
    );

    return new JwtSecurityTokenHandler().WriteToken(token);
}

```

E depois no endpoint de Login de Administrador:
```C#
app.MapPost("/administradores/login", ([FromBody] LoginDTO loginDTO, IAdministradorServico administradorServico) => {
    var adm = administradorServico.Login(loginDTO);
    if(adm != null) 
    {
        string token = GerarTokenJWt(adm);

        return Results.Ok(new AdministradorLogado{
            Email = adm.Email,
            Perfil = adm.Perfil,
            Token = token
        });
    }
    else 
        return Results.Unauthorized();
}).WithTags("Administradores");
```
Se você notar, temos uma classe `AdministradorLogado`. Que foi uma `modelView` que criamos para usar aqui.

Ela ficou assim:
```C#
namespace MinimalApi.Dominio.ModelViews;

public record AdministradorLogado{
    public string Email { get; set; } = default!;
    public string Perfil { get; set; } = default!;
    public string Token { get; set; } = default!;
}
```

E pronto, acredito que seja só isso pra ser gerado um token no momento de criação do perfil.

---
#### Configurando Swagger para a passagem de token JWT

Precisamos configurar o Swagger, porque se não, teremos o Token gerado, mas não poderemos envia-lo para outros itens.

Então, lá nos builders, vamos nessa linha de código:
```C#
builder.Services.AddSwaggerGen();
```

E vamos transforma-la nisso:
```C#
builder.Services.AddSwaggerGen(options => {
    options.AddSecurityDefinition("Bearer", new OpenApiSecurityScheme{
        Name = "Autorization",
        Type = SecuritySchemeType.Http,
        Scheme = "bearer",
        BearerFormat = "JWT",
        In = ParameterLocation.Header,
        Description = "Insira o token JWT desta maneira: Bearer {Seu token}"
    });
    options.AddSecurityRequirement(new OpenApiSecurityRequirement{
        {
            new OpenApiSecurityScheme{
                Reference = new OpenApiReference{
                    Type = ReferenceType.SecurityScheme,
                    Id = "Bearer"
                }
            },
            new string[] {}
        }
    });
});
```
Lá no Swagger, as rotas que precisam de autenticação ficam com um cadeado na direta, lá no final do endpoint.


Depois, para permitirmos que não seja necessário autenticação para acessar determinada rota:
```C#
app.MapPost("/administradores/login", ([FromBody] LoginDTO loginDTO, IAdministradorServico administradorServico) => {
    var adm = administradorServico.Login(loginDTO);
    if(adm != null) 
    {
        string token = GerarTokenJWt(adm);

        return Results.Ok(new AdministradorLogado{
            Email = adm.Email,
            Perfil = adm.Perfil,
            Token = token
        });
    }
    else 
        return Results.Unauthorized();
}).AllowAnonymous().WithTags("Administradores");
//Colocamos esse AllowAnonymous
```

---
#### Criando autorização com perfil de Adm e Editor

Até agora, mexemos com Autenticação, agora iremos mexer com autorização:

Mudamos aqui:
```C#
var claims = new List<Claim>()
    {
        new Claim("Email", administrador.Email),
        new Claim("Perfil", administrador.Perfil),
        //Aqui em baixo:
        new Claim(ClaimTypes.Role, administrador.Perfil)
    };
```

Também adicionamos quais os ***Roles*** que podem acessar determinadas rotas e endpoints:
```C#
app.MapPost("/veiculos", ([FromBody] VeiculoDTO veiculoDTO, IVeiculoServico veiculoServico) => {

//Tirei o código dessa brincadeira, pra economizar espaço})

    .RequireAuthorization()
    //Esse por exemplo, tanto Adm quanto Editor pode mexer.
    .RequireAuthorization(new AuthorizeAttribute { Roles = "Adm,Editor"})
    .WithTags("Veiculos");
```

---
#### Refatorando projeto criando sln e projeto de test

1. Criamos uma pasta chamada `Api` no root do projeto. Depois tacamos todos os arquivos, menos o `.gitignore`.
	
	- Rodamos os comandos:
		- `dotnet new sln`
		- `dotnet sln add Api/minimal-api.csproj`
	
	O que fizemos, foi criar uma nova solution, e referenciar a outra que tínhamos na nova solution.

Se você der um `dotnet new list` ele mostra todos os boilerplates que temos.

2. Nós iremos criar um novo projeto para testes:
	- `dotnet new mstest -o Test`

3. Agora adicionaremos esse novo projeto Test, à nossa solution raiz:
	- `dotnet sln add Test/Test.csproj`

4. Depois entraremos no diretório com `cd Test/` e depois referenciaremos a nossa `Api` no nosso projeto de Testes:
	- `dotnet add reference ../Api/minimal-api.csproj`

---
#### Criando teste de unidade para modelo de Administrador
*Parece que esses são testes para as entidades (no caso para administrador)*

Deletamos o `UnitTest1.cs` e criamos uma pasta chamada `Domain` no root e colocamos uma classe de testes chamada `AdministradorTest.cs`

Temos 3 fases quando vamos fazer nossos testes:

- Arrange 
	- Todas as variáveis que vamos criar para fazer as validações
- Act
	- A ação que vamos executar devido ao item ou validação que vamos fazer
- Assert
	- Onde vamos fazer a validação desses dados

```C#
using minimalApi.Dominio.Entidades;

namespace Test.Domain.Entidades;

[TestClass]
public class AdministradorTest
{
    [TestMethod]
    public void TestarGetSetPropriedades()
    {
        // Arrange
        var adm = new Administrador();

        // Act
        adm.Id = 1;
        adm.Email = "teste@teste.com";
        adm.Senha = "teste";
        adm.Perfil = "Adm";

        // Assert
        Assert.AreEqual(1, adm.Id);
        Assert.AreEqual("teste@teste.com", adm.Email);
        Assert.AreEqual("teste", adm.Senha);
        Assert.AreEqual("Adm", adm.Perfil);
    }
}
```

- Nesse caso:
	- `adm` = instância da variável para teste
	- parte do `//Act` = teste do set
	- parte do `//Assert` = teste do get
		- `Assert.AreEqual("teste@teste.com", adm.Email);`
		- esperamos receber:
			- `"teste@teste.com"` na propriedade `adm.Email

- Depois dá um `dotnet test` que ele roda o teste

Agora, se por exemplo mudássemos de `Email` pra `Emais` sem querer na nossa entidade lá na nossa Api, o teste iria dar erro.

---
#### Testes de Persistência
*Parece que nesse caso vão ser para os serviços*

Esse aqui eu meio que pulei, mas o código ficou assim:

`Dominio/Servicos/AdministradorServico`
```C#
using System.Reflection;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Configuration;
using minimalApi.Dominio.Entidades;
using MinimalApi.Dominio.Servicos;
using MinimalApi.Infraestrutura.Db;

namespace Test.Domain.Entidades;

[TestClass]
public class AdministradorServicoTest
{
    private DbContexto CriarContextoDeTeste()
    {
        var assemblyPath = Path.GetDirectoryName(Assembly.GetExecutingAssembly().Location);
        var path = Path.GetFullPath(Path.Combine(assemblyPath ?? "", "..", "..", ".."));

        var builder = new ConfigurationBuilder()
            .SetBasePath(path ?? Directory.GetCurrentDirectory())
            .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
            .AddEnvironmentVariables();

        var configuration = builder.Build();

        return new DbContexto(configuration);
    }


    [TestMethod]
    public void TestandoSalvarAdministrador()
    {
        // Arrange
        var context = CriarContextoDeTeste();
        context.Database.ExecuteSqlRaw("TRUNCATE TABLE Administradores");

        var adm = new Administrador();
        adm.Email = "teste@teste.com";
        adm.Senha = "teste";
        adm.Perfil = "Adm";

        var administradorServico = new AdministradorServico(context);

        // Act
        administradorServico.Incluir(adm);

        // Assert
        Assert.AreEqual(1, administradorServico.Todos(1).Count());
    }

    [TestMethod]
    public void TestandoBuscaPorId()
    {
        // Arrange
        var context = CriarContextoDeTeste();
        context.Database.ExecuteSqlRaw("TRUNCATE TABLE Administradores");

        var adm = new Administrador();
        adm.Email = "teste@teste.com";
        adm.Senha = "teste";
        adm.Perfil = "Adm";

        var administradorServico = new AdministradorServico(context);

        // Act
        administradorServico.Incluir(adm);
        var admDoBanco = administradorServico.BuscaPorId(adm.Id);

        // Assert
        Assert.AreEqual(1, admDoBanco?.Id);
    }
}
```

Too much complicated

---
#### Criando testes de request

#incompleto 