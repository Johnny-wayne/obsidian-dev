___
###### Conteúdo do curso:

Este curso, visa ensinar a manipular os elementos DOM usando JavaScript.

Precisamos com o JavaScript, sermos capazes de editar os atributos do nosso *robotron2000* aumentando a quantidade de braços, pernas, e etc, para que ele tenha mais chance de vencer.

---
#### Entendendo o DOM

Usamos a palavra "document" no console do navegador e entendemos que ela tem alguns poderes. Mas, afinal, o que é essa palavra?

Sempre que o JavaScript vai agir com o navegador, ele navega em uma coisa chamada [[DOM]]. 

DOM é a sigla de 

==**D**ocument 
**O**bject 
**M**odel==

Ou *modelo de objeto do documento*. O nosso HTML é um documento e para lê-lo o navegador o transforme em um objeto. Um objeto manipulável, um objeto na estrutura do JavaScript.

---

##### Métodos para selecionar elementos no HTML

- `document.getElementByID(id)` - Recupera um elemento pelo ID.
- `document.getElementsByTagName(name)` - Recupera um elemento pelo nome.
- `document.getElementsByClassName(name)` - Recupera um elemento pelo nome da classe.

##### Propriedades e métodos para alterar elementos no HTML

- `element.innerHTML` - Esta propriedade obtém ou altera qualquer elemento no HTML, inclusive tags.
- `element.innerText` - Esta propriedade permite inserir textos no HTML.
- `element.value` - Esta propriedade altera o valor de um elemento HTML
- `element.setAttribute(atributo, valor)` - Este método altera o valor de um atributo de um elemento HTML.

##### Adicionando e excluindo elementos

- `document.write()` - Escreve no fluxo de saída do HTML.
- `document.appendChild()` - Adiciona um elemento HTML.
- `document.removeChild()` - Remove um elemento HTML.
- `document.replaceChild()` - Substitui um elemento HTML.
- `document.createElement()` - Cria um elemento HTML.

---
#### Funções

##### Hoisting

Qual delas está certa?

```javascript
function myFunction() {
  document.querySelector("#retorna").innerHTML = "Confirma";
}

const elemento = document.querySelector("#botao");
elemento.addEventListener("click", myFunction);
```

```javascript
const elemento = document.querySelector("#botao");
elemento.addEventListener("click", myFunction);

function myFunction() {
  document.querySelector("#retorna").innerHTML = "Confirma";
}
```

Ambas, isso acontece devido ao comportamento de [[hoisting]] no JavaScript.

##### Funções nomeadas

Este é um exemplo de *função nomeada* ou o que chamamos de *declaração de uma função*
```js
const robotron = document.querySelector("#robotron")
robotron.addEventListener("click", dizOi);

function dizOi() {
    console.log("oi");
}
```

Mas não é a única forma de se declarar funções. Existe uma outra forma, chamada de *função anônima*, ou seja, uma função sem nome.

Pode ser feita dessa forma:
```js
const robotron = document.querySelector("#robotron")
robotron.addEventListener("click", function() {
	console.log("diz oi")
});
```

```js
function() {
    // Function Body
}
```

Ou dessa forma:
```js
const robotron = document.querySelector("#robotron")
robotron.addEventListener("click", () => {
	console.log("diz oi")
});
```

```js
() => {
    // Function Body...
}
```

---
#### Reaproveitando código

```js
const controle = document.querySelectorAll(".controle-ajuste");

controle.forEach( (elemento) => {
    elemento.addEventListener( "click", (evento) => {
        console.log("funcionou");
    })
})
```

- `document.querySelectorAll(".controle-ajuste");` acaba por selecionar todos os elementos, cuja classe é igual a "controle-ajuste"
- o método [`forEach()`](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) pega cada

----
###### O código até agora

```js
//selecionamos todos os elementos que possuem a classe "controle ajuste"
//Ou seja todos os sinais de + e -
const operacaoAjuste = document.querySelectorAll(".controle-ajuste");

//para cada um desses elementos
//quando eles forem clicados
//passaremos como argumento as propriedades dos alvos dos elementos abaixo
operacaoAjuste.forEach( (element) => {
    element.addEventListener("click", (evento) => {
	    //manipulaDados(operacao, controleQtd)
        manipulaDados(evento.target.textContent, evento.target.parentNode)
    })
})

//pegamos os argumentos passados anteriormente
function manipulaDados(operacao, controleQtd) {

	//"controle-contador" é a parte onde são apresentados os números
    qtd = controleQtd.querySelector(".controle-contador");
 
    if(operacao === "-") {
	    //o valor vem em string, então transformamos ele me inteiro e somamos
        qtd.value = parseInt(qtd.value) - 1;
    } else {
        qtd.value = parseInt(qtd.value) + 1;
    }
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="shortcut icon" type="image/jpg" href="img/favicon.ico"/>
    <title>Robotron 2000</title>

    <link rel="stylesheet" href="css/style.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Teko:wght@300;500&display=swap" rel="stylesheet">
</head>
<body>
    <main>
        <section class="robotron">
            <img class="robo" src="img/robotron.png" alt="Robotron" id="robotron">
            <figcaption class="titulo">ROBOTRON <br>2000</figcaption>
        </section>
  
        <section class="box estatisticas">
            <div class="estatistica">
                <p class="estatistica-titulo">Força</p>
                <div class="estatistica-valor">
                    <p class="estatistica-numero">768</p>
                </div>
            </div>
            <div class="estatistica">
                <p class="estatistica-titulo">Poder</p>
                <div class="estatistica-valor">
                    <p class="estatistica-numero">630</p>
                </div>
            </div>
            <div class="estatistica">
                <p class="estatistica-titulo">Energia</p>
                <div class="estatistica-valor">
                    <p class="estatistica-numero">289</p>
                </div>
            </div>
            <div class="estatistica">
                <p class="estatistica-titulo">Velocidade</p>
                <div class="estatistica-valor">
                    <p class="estatistica-numero">597</p>
                </div>
            </div>
        </section>
  
        <section class="equipamentos">
            <form action="" class="montador">
                <div class="box montador-conteudo">
                    <div class="peca">
                        <label for="" class="peca-titulo">Braços</label>
                        <div class="controle">
                            <buttom class="controle-ajuste">-</buttom>
                            <input type="text" class="controle-contador" value="00">

                            <buttom class="controle-ajuste">+</buttom>
                        </div>
                    </div>
                    <hr class="linha">
                    <div class="peca">
                        <label for="" class="peca-titulo">Blindagem</label>
                        <div class="controle">
                            <buttom class="controle-ajuste">-</buttom>
                            <input type="text" class="controle-contador" value="00">
                            <buttom class="controle-ajuste">+</buttom>
                        </div>
                    </div>
                    <hr class="linha">
                    <div class="peca">
                        <label for="" class="peca-titulo">Núcleos</label>
                        <div class="controle">
                            <buttom class="controle-ajuste">-</buttom>
                            <input type="text" class="controle-contador" value="00">
                            <buttom class="controle-ajuste">+</buttom>
                        </div>
                    </div>
                    <hr class="linha">
                    <div class="peca">
                        <label for="" class="peca-titulo">Pernas</label>
                        <div class="controle">
                            <buttom class="controle-ajuste">-</buttom>
                            <input type="text" class="controle-contador" value="00">
                            <buttom class="controle-ajuste">+</buttom>
                        </div>
                    </div>
                    <hr class="linha">
                    <div class="peca">
                        <label for="" class="peca-titulo">Foguetes</label>
                        <div class="controle">
                            <buttom class="controle-ajuste">-</buttom>
                            <input type="text" class="controle-contador" value="00">
                            <buttom class="controle-ajuste">+</buttom>
                        </div>
                    </div>
                </div>
                <input type="submit" value="Iniciar produção" class="producao" id="producao">
            </form>
        </section>
    </main>
    <script src="js/main.js"></script>
</body>
</html>
```

---
#### Data Attributes

> [!warning] problema
> As classes CSS estão acopladas com as classes que selecionamos no JS, isso se torna um problema quando precisamos alterar ou editar as classes CSS

Para resolver esse problema, nós usamos os **Data Atributtes**

```js
const controleAjuste = document.querySelectorAll("[data-controle]");
```