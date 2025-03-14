
#### `ngModel`

O `ngModel` é uma diretiva Angular que facilita a criação de formulários e a sincronização de dados entre a interface do usuário e a lógica da aplicação.

**Funcionalidades:**

- **Data binding bidirecional:** Vincula automaticamente o valor de um elemento HTML a uma propriedade do componente.
- **Validação:** Permite definir regras de validação para os campos do formulário.
- **Formatação:** Permite formatar a entrada e saída de dados.
- **Mensagens de erro:** Exibe mensagens de erro para campos inválidos.

---
###### **Exemplo:**

**HTML**
```html
<input type="text" [(ngModel)]="nome" />
```

**TypeScript**
```ts
export class AppComponent {
  nome = '';
}
```

---

Neste exemplo, a diretiva `ngModel` vincula o valor do campo de texto (`input`) à propriedade `nome` do componente. Quando o usuário altera o valor do campo de texto, a propriedade `nome` é atualizada automaticamente. Da mesma forma, quando a propriedade `nome` é alterada na lógica da aplicação, o valor do campo de texto é atualizado automaticamente.

---
**Vantagens:**

- Simplifica a criação de formulários.
- Sincronização automática de dados.
- Validação e formatação de dados.
- Exibição de mensagens de erro.


**Desvantagens:**

- Pode ser difícil de entender para iniciantes.
- Pode ser difícil de usar em formulários complexos.

> Em resumo, o `ngModel` é uma diretiva poderosa que facilita a criação de formulários e a sincronização de dados entre a interface do usuário e a lógica da aplicação.

---
**Recursos adicionais:**

- Documentação oficial do Angular: [https://angular.io/guide/forms-overview](https://angular.io/guide/forms-overview)
- Tutoriais sobre o `ngModel`: [https://www.youtube.com/watch?v=wHT8bGH_PGk](https://www.youtube.com/watch?v=wHT8bGH_PGk)