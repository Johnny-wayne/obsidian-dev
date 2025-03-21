Artigo relacionado à nota:
https://www.alura.com.br/artigos/hoisting-no-javascript

---
Quando uma equipe trabalha em algum projeto, muito provavelmente o código será lido e alterado por diversas pessoas, dessa maneira, é necessário entender diferentes formas possíveis de escrever o mesmo código, obtendo uma boa produtividade na sua performance de desenvolvimento.

Contudo, é importante para uma **pessoa programadora** entender o **que é Hoisting** e como se comporta em diferentes casos nesta linguagem.

Vamos analisar este **código de **function declaration****, e o que retorna:

```js
console.log(soma(2, 5))
function soma(a, b) {
return a + b
}
```

Este código retorna o valor: `7`

Repare que a função consegue ser chamada antes mesmo de ter sido declarada. **Hoisting** é o termo que explica essa situação, em português ele significa “içamento”, ou “elevação” e foi citado pela primeira vez no **[ECMAScript® 2015 Language Specification](https://262.ecma-international.org/6.0/)**. O Hoisting permite que você execute funções antes das suas declarações. Na prática, inicialmente as **declarações de funções** são colocadas na memória durante a [fase de compilação](https://www.alura.com.br/artigos/o-que-e-compilacao) e, mesmo assim, permanecem no mesmo lugar que estão digitadas.

A razão pela qual o código anterior funciona é que os mecanismos [JavaScript](https://www.alura.com.br/artigos/javascript) movem a função soma para o início do escopo, como ilustra o código abaixo:

```js
function soma(a,b){
    return a + b
}
console.log(soma(2,5))
```

Entretanto, será que Hoisting funciona em outros tipos de código? Vamos conferir!

```js
console.log(alura)
var alura = ‘cursos’;
```

Este código retorna:

```js
undefined
```

A utilização de **Hoisting em var não é indicada**, pois a variável criada é elevada para o escopo, mas sem o seu valor, e com isso, retorna valor `undefined`.

O comportamento é parecido utilizando também var function:

```js
function testaHoisting() {
    console.log(‘testaHoisting’, alura)
    var alura = ‘cursos’
}
```

Este código retorna: `undefined`.

**Hoisting também não é indicado utilizando let**, pois acontece um outro tipo de **comportamento não desejado:**

```js
console.log(alura)
let alura = ‘cursos’;
```

Este código retorna:

```js
script.js:1 Uncaught ReferenceError: Cannot access 'alura' before initialization´´´ // <-- os 3 pontos são ao contrário
```

Esta mensagem em português significa “Não é possível acessar ‘alura’ antes de sua inicialização'', ou seja, a linguagem JavaScript reconhece que `let = alura` existe, porém não consegue acessar sua declaração. Esse comportamento de Hoisting com `let` é o mesmo ao utilizar `const`.


---
Aqui tem um conteúdo mais "aprofundado":
https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
