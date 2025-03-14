## O que o comando `dotnet watch run` faz?

**Em poucas palavras:**

O comando `dotnet watch run` é uma ferramenta poderosa do .NET que automatiza o processo de desenvolvimento, **recompilando e reiniciando automaticamente seu aplicativo sempre que você fizer uma alteração no código-fonte**. Isso significa que você pode ver os resultados das suas modificações quase instantaneamente, agilizando significativamente o ciclo de desenvolvimento.

**Explicando em detalhes:**

- **Monitoramento de arquivos:** O `dotnet watch` funciona como um observador, constantemente monitorando os arquivos do seu projeto.
- **Detecção de alterações:** Quando você salva uma alteração em algum arquivo, o `dotnet watch` detecta essa modificação.
- **Execução do comando:** Em seguida, ele executa o comando especificado, que no caso do `dotnet watch run` é o comando `dotnet run`.
- **Recompilação e reinício:** O `dotnet run` recompila o seu projeto e reinicia a aplicação, permitindo que você veja as mudanças em tempo real.