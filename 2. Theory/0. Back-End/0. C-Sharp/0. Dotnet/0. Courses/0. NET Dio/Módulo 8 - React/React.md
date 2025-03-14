
---
## HTML, CSS e JavaScript

### Node e NPM

##### Node.js

Node.js é um runtime de JavaScript. Foi desenvolvido em cima do motor JavaScript V8 - engine criada pelo Google e utilizada nos navegadores Chrome.

###### NPM

O NPM (Node Package Manager), é o gerenciador de pacote padrão do node. Ele é utilizado como gerenciamento de pacotes, fluxo de trabalho em linguagens de programação e ferramenta para construção de front-ends em aplicativos e websites.

#### Yarn

O Yarn é um gerenciador de pacotes para aplicar comandos prontos ao código de uma aplicação.

`npm install -g yarn`


---
#### React DevTools

É uma extensão disponível para o Chrome, Firefox e outros, e também como um aplicativo independente que permite inspecionar a hierarquia de componentes do React nas ferramentas do desenvolvedor do navegador


---
#### Extensões VScode

- Por que utilizar extensões?
	Costumam ser leves, não comprometem o funcionamento do software e são de fácil instalação. Cada dev tem a sua maneira de programar e é por isso que as extensões podem ser ótimas aliadas! Com elas, conseguimos adaptar o VSCode às nossas necessidades, criando uma rotina de trabalho e estudo um ambiente mais funcional.

---
### Páginas Web com HTML

#### Meta Tags

Meta tags são linhas de código HTML ou "Etiquetas" que, entre outras coisas, descrevem o conteúdo do seu site para os buscadores. É nelas que você vai inserir as palavras-chave que facilitarão a vida do usuário na hora de te encontrar.

##### tags básicas

Essa por exemplo, é para as palavras-chave do site.
```html
<meta name="keywords" content="sites, web, desenvolvimento, html, design">
```

Descrição do site
```html
<meta name="description" content=" Meta Tags - O que são e como utilizá-las">
```

Linguagem da página
```html
<meta http-equiv="content-language" content="pt-br">
```

Tipo de conteúdo *(charset)*
```html
<meta http-equiv="content-type" content="text/html; charset=iso-8859-1">
```

Autor da página
```html
<meta name="author" content="Pablo Henrique">
```

Dá pra redirecionar por aqui também, 5 são os segundos e a url é o site de redirecionamento.
```html
<meta http-equiv="refresh" content="5;url=http://www.novosite.com/">
```


---

#### Formulários

O formulário HTML é um formulário de preenchimento de dados ou que resulta em uma ação desejada utilizando a linguagem de marcação HTML.  É formado por um ou mais campos. Esses campos podem ser de textos, caixas de seleção, botões, radio buttons e checkboxes utilizando tags do próprio HTML. Dessa forma, o usuário pode interagir com a página e executar ações através desse formulário.

```html
<h2>Formulário</h2>
	<div>
		<form action="" method="get">
			<div>
				<label for="none">Nome:</label>
				<br />
				<input type="text" id="nome" name="nome" />
			</div>
			<div>
				<label for="email">E-mail:</label>
				<br />
				<input type="email" id="email" name="email" />
			</div>
			<div>
				<label for="msg">Mensagem:</label>
				<br />
				<textarea type="text" id="msg" name="mensagem" />
			</div>
		</form>
	</div>
```

A linha mais importante aqui
```html
	<form action="" method="get">
```
- `Action` - é a ação que vai ser realizada,, pra onde a gente quer mandar as informações, provavelmente deve ser o nome de alguma função ou método, ou até mesmo uma URL, aqui a gente deixou vazio.
- `method` - Ele vai pegar todos os inputs, e passar pro action/URL

O recomendado para informações mais sensíveis, é usar o método `post`
```html
	<form action="" method="post">
```
Porque as informações com o `get` ficam muito visíveis pro usuário e na rede.

---
#### HTML Semântico

O HTML semântica é a forma de deixar o site com suas informações bem explicadas e compreensíveis para o computador, ajudando até mesmo em sua busca no Google e facilitando o entendimento de leitores de acessibilidade.

Além de facilitar a busca de forma orgânica e ranquear sua página em mecanismos de busca, o HTML semântico ajuda os leitores de tela para deficientes visuais, facilitando seu compreendimento. Ele, também, deixa seu código mais limpo e mais compreensível, tanto em organização como em facilidade de visualizar uma tag específica só de passar o olho pela tela.

---
### JavaScript

#### Métodos de array

Os métodos de array em JavaScript são ferramentas poderosas para manipular e transformar dados de forma eficiente. Vamos explorar cada um dos métodos que você mencionou:

**Em resumo:**

- **filter():** Cria um novo array com elementos que passam em um teste.
- **find():** Retorna o primeiro elemento que passa em um teste.
- **findIndex():** Retorna o índice do primeiro elemento que passa em um teste.
- **reduce():** Reduz um array a um único valor.
- **some():** Verifica se pelo menos um elemento passa em um teste.
- **every():** Verifica se todos os elementos passam em um teste.

**Quando usar cada um:**

- Use `filter()` para criar subconjuntos de um array.
- Use `find()` ou `findIndex()` para encontrar um elemento específico.
- Use `reduce()` para realizar cálculos acumulados.
- Use `some()` ou `every()` para verificar se um array satisfaz uma determinada condição.

##### filter()

- **Objetivo:** Criar um novo array com todos os elementos que satisfazem uma determinada condição.
- **Sintaxe:** `array.filter(callback(element, index, array))`

- **Exemplo:**
    ```    JavaScript
    const numeros = [1, 2, 3, 4, 5];
    const numerosPares = numeros.filter(numero => numero % 2 === 0); // [2, 4]
    ```

- **Explicação:** A função `filter()` itera sobre cada elemento do array e aplica a função de callback. Se a função de callback retornar `true` para um elemento, ele é incluído no novo array.

##### find()

- **Objetivo:** Retornar o **primeiro** elemento de um array que satisfaz uma determinada condição.
- **Sintaxe:** `array.find(callback(element, index, array))`

- **Exemplo:**        
    ``` JavaScript
    const pessoas = [
        { nome: 'João', idade: 30 },
        { nome: 'Maria', idade: 25 }
    ];
    const pessoaEncontrada = pessoas.find(pessoa => pessoa.nome === 'Maria'); // { nome: 'Maria', idade: 25 }
    ```

- **Explicação:** A função `find()` é similar ao `filter()`, mas ela para a iteração assim que encontra o primeiro elemento que satisfaz a condição e retorna esse elemento.

##### findIndex()

- **Objetivo:** Retornar o **índice** do **primeiro** elemento de um array que satisfaz uma determinada condição.
- **Sintaxe:** `array.findIndex(callback(element, index, array))`

- **Exemplo:**    
    ```JavaScript
    const frutas = ['maçã', 'banana', 'laranja'];
    const indiceDaBanana = frutas.findIndex(fruta => fruta === 'banana'); // 1
    ```

- **Explicação:** A função `findIndex()` é similar ao `find()`, mas em vez de retornar o elemento, ela retorna o índice do elemento encontrado.

##### reduce()

- **Objetivo:** Reduz um array a um único valor aplicando uma função a cada elemento.
- **Sintaxe:** `array.reduce(callback(accumulator, currentValue, currentIndex, array), initialValue)`

- **Exemplo:**    
    ```JavaScript
    const numeros = [1, 2, 3, 4];
    const soma = numeros.reduce((total, numero) => total + numero, 0); // 10
    ```

- **Explicação:** A função `reduce()` acumula um valor ao longo da iteração. O `initialValue` é o valor inicial do acumulador. A função de callback recebe o acumulador, o valor atual, o índice e o array original.

##### some()

- **Objetivo:** Verificar se pelo menos um elemento de um array satisfaz uma determinada condição.
- **Sintaxe:** `array.some(callback(element, index, array))`

- **Exemplo:**
    ```JavaScript
    const numeros = [1, 2, 3, 4, 5];
    const temNumeroPar = numeros.some(numero => numero % 2 === 0); // true
    ```

- **Explicação:** A função `some()` retorna `true` se pelo menos um elemento do array satisfaz a condição, caso contrário, retorna `false`.

##### every()

- **Objetivo:** Verificar se todos os elementos de um array satisfazem uma determinada condição.
- **Sintaxe:** `array.every(callback(element, index, array))`

- **Exemplo:**
    ```JavaScript
    const numeros = [1, 3, 5, 7];
    const todosSaoImpares = numeros.every(numero => numero % 2 !== 0); // true
    ```
 
- **Explicação:** A função `every()` retorna `true` se todos os elementos do array satisfazem a condição, caso contrário, retorna `false`.

---
### Entendendo o DOM

Entender o que é o DOM *(Documento Object Model)* e como é manipulado usando JavaScript.

O DOM é a representação de dados dos objetos que compõem a estrutura e o conteúdo de um documento na Web. O DOM é uma interface de programação para os documentos HTML e XML. Representa a página de forma que os programas possam alterar a estrutura do documento, alterar o estilo e conteúdo. O DOM representa o documento com nós e objetos.

![[Pasted image 20241115002508.png]]

---
#### Manipulando a DOM com JavaScript

O DOM não é uma linguagem de programação, mas sem ele, a linguagem JavaScript não teria nenhum modelo ou noção de páginas web, páginas XML e elementos com os quais ela geralmente lida. Cada elemento de um documento faz parte do Document Object Model, para que possam ser acessados e manipulados usando o DOM e uma linguagem de script, como JavaScript

---
## React

### Introdução
#### O que é React

- A história do React
	React JS é uma biblioteca JavaScript para a criação de interfaces de usuário. Criado em 2011 pelo time do Facebook, o React surgiu com o objetivo de otimizar a atualização e a sincronização de atividade simultâneas no feed de notícias de rede social, entre eles chat, status, listagem de contatos e outros.
	
	A princípio, todas essas atividades, chamadas de estados, tinham uma descrição muito complexa. Com o React, esta descrição torna-se mais simples, bem como também é simplificada a conexão entre HTML, CSS e JavaScript e todos os componentes de uma página.
	
	Por ter demonstrado grande eficiência, nos anos que se surgiram o React foi incorporado à interface de outras redes sociais do grupo, como o Instagram, e em 2013, seu código foi aberto à comunidade, dando início a sua popularização

---
#### Biblioteca

Esse é o recurso mais utilizado no mundo da programação e muitas pessoas nem se dão conta do quanto utilizam. A ideia da biblioteca é compartilhar soluções por meio de funções ou métodos. Por exemplo: Se você tiver que fazer um trabalho de matemática, poderá ir até uma biblioteca física, pegar um livro e utilizar equações desenvolvidas no livro. Então, não será preciso desenvolver as equações desde o início.

- Exemplo de Bibliotecas:
	- Moment.js
	- Chart.js
	- Voca
	- mo.js
	- React

#### Frameworks

O framework nada mais é do que uma ferramenta que vai te ajudar a ter como único objetivo focar em desenvolver o projeto, não em detalhes de configurações.

- Angular
- Vuex
- Ionic
- Next
- Express
- LoopBack

---
#### Criando projeto React

Solta um `npx create-react-app dio` pra criar um app react chamado dio.

Ele vai nos dar uma estrutura de pastas e arquivos inicial contendo isso aqui:
![[Pasted image 20241115170005.png]]

- `node_modules` - vai ter todas as bibliotecas, dependências que vamos utilizar no nosso projeto. Tudo fica naquela pasta ali e a gente não mexe.

- `public` - os arquivos iniciais principais do React, porque ele trabalha com uma estrutura chamada PWA, ou renderização lado cliente. Cada página da nossa aplicação vai ser como um componente que vai ser renderizado conforme navegamos.  Então pra isso, ele sempre vai colocar isso no nosso `index.html`.

- É nesse pedaço do nosso `index.html` que a mágica do React vai acontecer:
	```html
	<body>
		<noscript>You need to enable JavaScript to run this app.</noscript>
		<div id="root"></div>
	</body>
	```

- A gente sabe disso porque no arquivo `index.js` nós temos:
```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

//Ó o tal do root aqui:
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

reportWebVitals();
```

- React manipula DOM

- `package.json` - onde teremos todas as nossas dependências

`scr/App.js`
```jsx

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```
Um componente nada mais é que uma função retornando este HTML. E esse HTML dentro de uma função tem outro nome chamado [[JSX]]. O JS faz a conversão pra gente, mas eles tem algumas diferencinhas, como em vez de `class`, nesse caso usamos `className`.

Mudamos um pouco pra deixar mais clean, mas se vc for ver, essa função/component `App`:
```jsx
function App() {
  return (
    <div className="App">
      Hello World!
    </div>
  );
}
```

É chamado no nosso `index.js`:
```jsx
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
	//aqui ó
    <App />
  </React.StrictMode>
);
```

---
#### Componentes de classes x funcionais

Antes o React usava classes para criar componentes em vez de funções.

Antes a parada era assim:
```jsx
import React, {Component} from "react";

export default class AppClass extends Component {
    constructor(props) {
        super(props);
        this.state = { counter: 0 };
        this.handleClick = this.handleClick.bind(this);
    }

    handleClick() {
        //TODO
    }
    render() {
        return <div>AppClass</div>;
    }
}
```

Agora é assim:
```jsx
function App() {
  return (
    <div className="App">
      Hello World!
    </div>
  );
}

export default App;

```

---
#### Conceitos de componentes e props

Vamos criar uma pasta `components` dentro da pasta `src` e dentro dessa nova pasta, vamos criar outra pasta chamada `Button` e normalmente eles nomeiam o arquivo JS que vai ser escrito o component como `index.js` mesmo. Pra evitar redundância nos imports.

Como por exemplo: 
	`import Button from 'Button/button.js`
	E em vez disso:
	`import Button from 'Button/index.js`

Passando pra criação do component:
```jsx
export default function Button() {
	return {
		<div>index</div>
	}
}
```

Precisamos exportar porque queremos que outros lugares possam importar esse botão.

Agora vamos passar propriedades:
```jsx
export default function Button({title}) {
	return {
		<div>{title}</div>
	}
}
```

Nós passamos dentro de chaves para fazer algo chamado de [[destructuring assignment]], se não desestruturássemos. Precisaríamos fazer algo como:
```jsx
export default function Button(props) {
	const { title } = props
	return {
		<div>{title}</div>
	}
}
```