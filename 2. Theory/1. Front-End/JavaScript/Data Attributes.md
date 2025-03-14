
Os _data attributes_ (atributos de dados) em JavaScript são uma forma de adicionar dados personalizados a elementos HTML. Esses dados podem ser acessados e manipulados usando JavaScript, permitindo adicionar comportamento dinâmico às páginas web.

### Estrutura dos Data Attributes

Os data attributes são definidos em elementos HTML com o prefixo `data-`. O nome do atributo deve começar com `data-` seguido de um nome personalizado. Por exemplo:

html

Copy code

```js
<div id="meuElemento" data-usuario="João" data-idade="30"></div>
```

Nesse exemplo, o elemento `<div>` tem dois data attributes: `data-usuario` com o valor "João" e `data-idade` com o valor "30".

### Acessando Data Attributes com JavaScript

Para acessar os data attributes em JavaScript, usamos a propriedade `dataset` do elemento. Essa propriedade é um objeto onde cada data attribute é uma propriedade do objeto.

##### Exemplo:

```js
// Seleciona o elemento com id "meuElemento" 
let elemento = document.getElementById('meuElemento'); 

// Acessa os data attributes 
let usuario = elemento.dataset.usuario; // "João" 
let idade = elemento.dataset.idade; // "30"  

console.log(usuario); // Output: João 
console.log(idade); // Output: 30
```


### Modificando Data Attributes com JavaScript

Também é possível modificar os valores dos data attributes usando a mesma propriedade `dataset`.

##### Exemplo:


```js
// Modifica os data attributes 
elemento.dataset.usuario = "Maria"; 
elemento.dataset.idade = "25";  

console.log(elemento.dataset.usuario); // Output: Maria 
console.log(elemento.dataset.idade); // Output: 25`

```

### Usos Comuns dos Data Attributes

1. **Armazenar Dados**: Facilita o armazenamento de informações diretamente no HTML, como IDs, estados ou configurações, sem precisar de variáveis globais ou consultas constantes ao servidor.
    
2. **Interação com CSS**: Pode ser usado para aplicar estilos personalizados baseados nos valores dos data attributes usando seletores CSS avançados.
    
3. **Melhorar a Manutenção do Código**: Facilita a manutenção, pois os dados estão diretamente associados aos elementos HTML, tornando o código mais legível e fácil de entender.
    

### Vantagens dos Data Attributes

- **Simplicidade**: Fácil de entender e implementar.
- **Flexibilidade**: Pode armazenar qualquer tipo de dado, desde números até strings complexas.
- **Manutenção**: Dados são auto-contidos nos elementos, o que facilita a manutenção e compreensão do código.

### Limitações

- **Validação**: Não há validação automática dos dados armazenados, então é preciso implementar verificações no JavaScript.
- **Desempenho**: Para páginas muito grandes ou com muitos data attributes, pode haver impacto no desempenho ao acessar e modificar esses atributos frequentemente.

### Exemplo Prático

Imagine que você tem uma lista de produtos e quer armazenar o ID e o preço de cada produto diretamente nos elementos HTML:

```html
<ul>   
	<li data-id="1" data-preco="19.99">Produto 1</li>   
	<li data-id="2" data-preco="29.99">Produto 2</li>   
	<li data-id="3" data-preco="39.99">Produto 3</li> 
</ul>
```

Representação:
<ul>   
	<li data-id="1" data-preco="19.99">Produto 1</li>   
	<li data-id="2" data-preco="29.99">Produto 2</li>   
	<li data-id="3" data-preco="39.99">Produto 3</li> 
</ul>

Com JavaScript, você pode facilmente acessar e utilizar esses dados:

---

```js
let produtos = document.querySelectorAll('li');  

produtos.forEach(produto => {   
	let id = produto.dataset.id;   
	let preco = produto.dataset.preco;      
	console.log(`Produto ID: ${id}, Preço: ${preco}`); 
});
```

### Conclusão

Os data attributes em JavaScript são uma ferramenta poderosa para adicionar e manipular dados personalizados em elementos HTML. Eles simplificam o desenvolvimento de aplicações web dinâmicas, permitindo um armazenamento de dados direto e fácil de acessar.