*Node Pack Manager*

---
npm cli normalmente vem junto com o [[Node]]

- `npm ls` - mostra todos os pacotes instalados
- `npm r NomeDoPacote` - remover pacote
- `npm i NomeDoPacote`


##### Json - JavaScript Object Notation

Para gerenciar os pacotes, documentar o projeto e automatizar alguns serviços, o Node gera um arquivo do tipo json. o `package.json`.

json é um modelo de arquivo usado para armazenamento e transmissão de dados no formato texto. Ele é usado em aplicações web pra estruturar informações.

Basicamente um documento json define um rotulo para cada valor apresentado usando delimitadores em cadeia: `{} [] ""`

Pra gerar o `package.json`, roda `npm init`

Depois de você instalar uma dependência, vai ser criado um novo arquivo `.json` chamado  `package-lock.json` que é um arquivo de segurança que garante que você vai instalar exatamente as mesmas versões das dependências quando vc for fazer um backup ou então publicar seu projeto.



---
Para importar um pacote em Node, você faz:

```javaScript
const nome = require('pacote')
```
