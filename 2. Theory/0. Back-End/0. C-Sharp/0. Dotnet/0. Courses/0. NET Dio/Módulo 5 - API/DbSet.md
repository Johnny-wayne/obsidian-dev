Anterior: [[Introdução as API's com C-sharp#Criando o Contexto | Criando um Context]]
Complemento [[DbContextOptions]]

---
**Classe Context usada**
```C#
using API_Desafio.Entities;
using Microsoft.EntityFrameworkCore;

namespace API_Desafio.Context
{
    public class DesafioContext : DbContext
    {
        public DesafioContext(DbContextOptions<DesafioContext> options): base(options)
        {

        }

        public DbSet<Tarefa> Tarefa{ get; set; }
    }
}
```

### O que é `DbSet<T>`?

Em C#, especialmente no contexto do ***Entity Framework Core***, o `DbSet<T>` representa uma coleção de [[Introdução as API's com C-sharp#Criando a classe entidade |entidades]] de um determinado tipo. É uma representação de uma tabela em um banco de dados relacional, permitindo que você execute operações de CRUD (Create, Read, Update, Delete) diretamente no código.

- `**DbSet`:** Indica que se trata de um conjunto de entidades.

- `<T>`: É um parâmetro de tipo genérico, que define o tipo específico das entidades que a coleção conterá. No caso de `DbSet<Tarefa>`, significa que a coleção conterá objetos do tipo `Tarefa`.

**Por que usar <> e colocar um tipo dentro?**

- **Tipagem forte:** Ao especificar o tipo `Tarefa` dentro dos colchetes, você garante que a coleção só conterá objetos desse tipo, evitando erros de tipo em tempo de compilação.

- **Reutilização:** O uso de genéricos permite criar classes e métodos mais flexíveis e reutilizáveis, pois podem trabalhar com diferentes tipos de dados.

- **Melhora a legibilidade:** Torna o código mais claro e intuitivo, pois o tipo da coleção é explicitamente declarado.

