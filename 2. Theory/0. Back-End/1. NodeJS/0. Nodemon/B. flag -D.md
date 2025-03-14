---
Id: 2.0.1.0.B
---

Diferença entre `npm install -D nodemon` e `npm install nodemon`

#### `npm install nodemon`

- **Instalação:** Adiciona o pacote `nodemon` como uma dependência **de desenvolvimento** do seu projeto.

- **Localização:** O pacote será instalado no diretório `node_modules` dentro do seu projeto.

- **Uso:** Pacotes de desenvolvimento são geralmente ferramentas que auxiliam no desenvolvimento, como linters, compiladores, servidores de desenvolvimento (como o [[A. Nodemon]]), etc. Eles não são necessários para executar a aplicação em produção.

### `npm install -D nodemon`

- **Instalação:** É exatamente a mesma coisa que `npm install nodemon`. O flag `-D` é um atalho para `--save-dev`.

- **Sinônimo:** Os dois comandos são sinônimos e produzem o mesmo resultado.

**Por que usar `-D`?**

- **Organização:** ==Ao usar `-D`, você mantém suas dependências de desenvolvimento separadas das dependências de produção.== Isso facilita a organização do seu projeto e a criação de ambientes mais limpos para produção.

- **Gerenciamento:** Quando você compartilhar seu projeto com outros desenvolvedores ou deployá-lo em um servidor, as dependências de desenvolvimento não são incluídas, evitando o envio de arquivos desnecessários.

**Em resumo:**

- **`npm install nodemon`:** Instala o Nodemon como uma dependência de desenvolvimento.
- **`npm install -D nodemon`:** É a mesma coisa que o comando anterior, apenas com um flag adicional para indicar que se trata de uma dependência de desenvolvimento.

**Quando usar qual?**

- **`-D`:** Use quando o pacote for necessário apenas durante o desenvolvimento, como ferramentas de build, linters, servidores de desenvolvimento, etc.
- **Sem `-D`:** Use quando o pacote for necessário para executar a aplicação em produção.

**Exemplo:**

Bash

```bash
# Instala o Nodemon como dependência de desenvolvimento
npm install -D nodemon

# Para iniciar o servidor com o Nodemon
npx nodemon app.js
```

Use o código [com cuidado](/faq#coding).

**Observação:**

- **`npx`:** Esta ferramenta é usada para executar pacotes localmente, sem a necessidade de instalá-los globalmente. É uma forma mais segura e recomendada de executar ferramentas como o Nodemon.

**Em conclusão:**

Ao utilizar o flag `-D` ao instalar o Nodemon, você garante que ele seja instalado como uma dependência de desenvolvimento, o que é a forma correta de adicionar ferramentas como essa ao seu projeto.