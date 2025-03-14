Anterior: [[Introdução as API's com C-sharp#Criando o Contexto | Criando um Context]]
Complemento: [[DbSet]]

---

- **`DbContextOptions<T>`:** Representa as opções de configuração para o contexto do banco de dados. O parâmetro de tipo `T` indica o tipo do contexto, neste caso, `DesafioContext`.

- **`: base(options)`:** Chama o construtor da classe base `DbContext`, passando as opções de configuração.