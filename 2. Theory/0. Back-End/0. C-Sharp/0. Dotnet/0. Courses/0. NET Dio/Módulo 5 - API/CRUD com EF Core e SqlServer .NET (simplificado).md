
## CRUD com EF Core e SqlServer em C# .NET: Um Guia Completo

Este guia te levará passo a passo na criação de um CRUD completo em um banco de dados SqlServer, usando a estrutura de dados Entity Framework Core (EF Core) e a linguagem C# no .NET.

---
### 1. Configurando o Ambiente

**1.1. Novo Projeto .NET:**

- Abra o Visual Studio e crie um novo projeto do tipo "Console App (.NET 6)" ou similar.
    
- Instale o pacote NuGet `Microsoft.EntityFrameworkCore.SqlServer` e, se precisar, o `Microsoft.EntityFrameworkCore.Tools`.
    

**1.2. Criando um Banco de Dados:**

- Se você não tiver um banco de dados existente, crie um novo banco de dados no SqlServer. Use o SQL Server Management Studio (SSMS) para esta tarefa.
    

---
### 2. Definindo a Entidade (Entity)

**2.1. Crie uma classe que represente a tabela do banco de dados:**

```C#
public class Produto
{
	[Key]
    public int Id { get; set; }
    public string Nome { get; set; } = string.Empty;
    public decimal Preco { get; set; }
    public int QuantidadeEmEstoque { get; set; }
}
```

**2.2. Atributos:**

- A classe Produto representa uma entidade que será mapeada para uma tabela no banco de dados.
    
- Cada propriedade da classe representa uma coluna da tabela.
    
- O atributo [Key] na propriedade Id indica que ela é a chave primária da tabela.
    

---
### 3. Criando o Contexto (DbContext)

**3.1. Crie uma classe que herda de DbContext:**

```C#
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options)
    {
    }

    public DbSet<Produto> Produtos { get; set; }
}
```


**3.2. Explicação:**

- A classe `AppDbContext` é o contexto do EF Core, responsável por gerenciar a interação com o banco de dados.
    
- A propriedade Produtos do tipo `DbSet<Produto>` representa um conjunto de objetos Produto que serão mapeados para a tabela "Produtos" no banco de dados.
    

---
### 4. Configurando a Conexão com o Banco de Dados

**4.1. Adicione a configuração da conexão ao banco de dados no arquivo appsettings.json:**

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=MeuBancoDeDados;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
}
```


**4.2. Configure o DbContext no arquivo Program.cs:**

```C#
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));

// ...
```


**4.3. Explicação:**

- O DbContext usa a string de conexão definida em `appsettings.json` para se conectar ao banco de dados.
    
- O método `UseSqlServer()` indica que o banco de dados é do tipo SqlServer.
    

---
### 5. Migrações (Migrations)

**5.1. Gerar Migrações:**

- Execute o comando `dotnet ef migrations add InitialCreate` na linha de comando do projeto.
    

**5.2. Criar a Tabela no Banco de Dados:**

- Execute o comando `dotnet ef database update` na linha de comando do projeto.
    

**5.3. Explicação:**

- As Migrações são ferramentas do EF Core que permitem automatizar o processo de criação e alteração de tabelas no banco de dados.
    
- O comando dotnet ef migrations add cria um script de migração que descreve as alterações a serem realizadas no banco de dados.
    
- O comando dotnet ef database update aplica os scripts de migração ao banco de dados, criando as tabelas e outras estruturas.
    

---
### 6. Implementação do CRUD

#### 6.1. Criar (Create):

```C#
public void CriarProduto(Produto produto)
{
    using var db = new AppDbContext(_contextOptions);
    db.Produtos.Add(produto);
    db.SaveChanges();
}
```

content_copyUse code [with caution](https://support.google.com/legal/answer/13505487).C#

**Explicação:**

- O método CriarProduto recebe um objeto Produto como parâmetro.
    
- O contexto AppDbContext é usado para adicionar o novo produto ao conjunto de objetos Produtos.
    
- O método SaveChanges() persiste as alterações no banco de dados.
    

#### 6.2. Ler (Read):

```C#
public List<Produto> ListarProdutos()
{
    using var db = new AppDbContext(_contextOptions);
    return db.Produtos.ToList();
}

public Produto BuscarProdutoPorId(int id)
{
    using var db = new AppDbContext(_contextOptions);
    return db.Produtos.Find(id);
}
```

content_copyUse code [with caution](https://support.google.com/legal/answer/13505487).C#

**Explicação:**

- O método ListarProdutos retorna uma lista de todos os produtos.
    
- O método BuscarProdutoPorId retorna um único produto pelo seu ID.
    

#### 6.3. Atualizar (Update):

```C#
public void AtualizarProduto(Produto produto)
{
    using var db = new AppDbContext(_contextOptions);
    db.Entry(produto).State = EntityState.Modified;
    db.SaveChanges();
}
```

content_copyUse code [with caution](https://support.google.com/legal/answer/13505487).C#

**Explicação:**

- O método AtualizarProduto recebe um objeto Produto com os dados atualizados.
    
- O método Entry(produto).State = EntityState.Modified indica que o objeto deve ser atualizado no banco de dados.
    
- O método SaveChanges() persiste as alterações.
    

#### 6.4. Deletar (Delete):

```C#
public void DeletarProduto(int id)
{
    using var db = new AppDbContext(_contextOptions);
    var produto = db.Produtos.Find(id);
    if (produto != null)
    {
        db.Produtos.Remove(produto);
        db.SaveChanges();
    }
}
```


**Explicação:**

- O método DeletarProduto recebe o ID do produto a ser removido.
    
- O contexto busca o produto pelo ID.
    
- Se o produto for encontrado, ele é removido do conjunto de objetos Produtos.
    
- O método `SaveChanges()` persiste a exclusão.
    


---
### 7. Integração Completa

**7.1. Implementar a lógica do CRUD:**

- Crie uma classe com os métodos CRUD que você implementou acima.
    
- Injete a dependência do contexto AppDbContext na classe.
    

**7.2. Criar um Menu para Interagir com o CRUD:**

- Crie um menu de opções no seu aplicativo console para o usuário interagir com o CRUD.
    
- Use os métodos do CRUD para executar as ações selecionadas pelo usuário.
    

### 8. Exemplo Completo:

```C#
using Microsoft.EntityFrameworkCore;

// ... outras imports

public class ProdutoService
{
    private readonly DbContextOptions<AppDbContext> _contextOptions;

    public ProdutoService(DbContextOptions<AppDbContext> contextOptions)
    {
        _contextOptions = contextOptions;
    }

    public void CriarProduto(Produto produto)
    {
        // ... 
    }

    public List<Produto> ListarProdutos()
    {
        // ... 
    }

    // ... demais métodos CRUD
}

class Program
{
    static void Main(string[] args)
    {
        // ... configurar o DbContext

        var produtoService = new ProdutoService(_contextOptions);

        // ... exibir menu e executar operações CRUD
    }
}
```

### 9. Considerações Adicionais:

- Este guia é um ponto de partida para construir um CRUD completo. Você pode adicionar funcionalidades como validação, tratamento de erros, segurança e outras features conforme a necessidade.
    
- O EF Core oferece diversas funcionalidades e recursos para você explorar, incluindo consultas complexas, relacionamentos entre entidades e muito mais.