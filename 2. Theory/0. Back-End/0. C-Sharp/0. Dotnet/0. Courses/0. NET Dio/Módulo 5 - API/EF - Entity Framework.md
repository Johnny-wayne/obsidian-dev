## O que é o EF Core?

O ***Entity Framework Core (EF Core)*** é uma ferramenta ***ORM (Object-Relational Mapper)*** da Microsoft que facilita a interação entre aplicações .NET e bancos de dados relacionais.

Em vez de escrever longas e complexas consultas SQL, você define classes (chamadas de **entidades**) que representam as tabelas do seu banco de dados. O EF Core se encarrega de traduzir essas classes em consultas SQL e de mapear os resultados para objetos .NET.

---
## O que são Entidades?

As **entidades** são classes que representam as tabelas do seu banco de dados. Cada propriedade de uma entidade corresponde a uma coluna da tabela. Por exemplo, se você tem uma tabela "Produtos", você criaria uma classe "Produto" com propriedades como "Id", "Nome" e "Preco".

**Exemplo de uma entidade:**
```C#
public class Produto
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public decimal Preco { get; set; }
}
```

