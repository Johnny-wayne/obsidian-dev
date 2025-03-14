Roadmap: https://roadmap.sh/javascript

- ECMAScript

---
#### Interpretador JavaScript

- V8 - Google

---
##### Sintaxe JS

- **Sentenças**
	Ele trabalha com conceito de Sentenças
	
	É mais fácil ver o exemplo do que explicar:
	
	- Tá certo, funciona de boa
	```javascript
	console.log("Sintaxe básica")
	console.log
	("Sintaxe básica 2")
	```
	
	- Tá errado, dá erro
	```javascript
	console.log("Sintaxe
		básica")
	```
	
	- O ponto e vírgula no final da sentença é opcional
	- A gente pode usar aspas ou aspas simples
	

- **Blocos**
	Ele também pode trabalhar com o conceito de blocos, sendo separados por chaves
	
	```javaScript
	{
		console.log("blocos");
	}
	```

---
#### Tipagem Dinâmica

1. Concatenação
	```javascript
	let nome = "Batman Bruce";
	
	//Não é recomendado utilizar dessa forma
	console.log("Aluno: " + nome) 
	
	//E sim dessa
	console.log(`Aluno: ${nome}`)
	
	```

2. Operações
```javascript
//Atenção!
console.log("3" + 2) // 32
console.log("3" - 2) // 1
//isso vale para os demais operadores
console.log("3" * 2) // 6
console.log("3" / 2) // 1.5
```

```javascript
console.log("3x" - 2) //NaN - Não existe
console.log(NaN === NaN) // false
```
Existe uma certa falta de precisão quando fazemos operações com números não inteiros.

Por exemplo:
```javascript
console.log(0.5 + 0.5) // 1
console.log(0.1 + 0.2) // 0.3000000000000004
console.log(0.1 + 0.7) // 0.7999999999999999
```

É como se ele escolhesse um tipo de variável diferente considerando o tipo de operação que vc tá fazendo.

```javascript
let sw = true
console.log(`Chave: ${sw}`) // Chave: true

let lamp = !0  // ! = NOT | 0 = false
console.log(typeof(lamp)) //boolean
console.log(`Lâmpada: ${lamp}`) //Lâmpada: true
```

Invertemos a lógica
```javascript
let sw = true
console.log(`Chave: ${sw}`) // Chave: true

let lamp = !1  // ! = NOT | 1 = true
console.log(typeof(lamp)) //boolean
console.log(`Lâmpada: ${lamp}`) //Lâmpada: false
```

---
#### Omitindo o uso de chaves nas estruturas de controle

##### If else

Estamos acostumados com isso
```javascript
let media = 4

if(media < 5) {
	console.log("REPROVADO")
	console.log("Não emitir certificado")
}

//output:
// REPROVADO
// Não emitir certificado
```

```javascript
let media = 4

if(media < 5) 
	console.log("REPROVADO")
	console.log("Não emitir certificado")

//output:
// Não emitir certificado
```

Em JavaScript, nós podemos omitir as chaves, só que apenas uma linha de código é vinculada a estrutura

Funciona certinho
```javascript
let media = 4

if(media < 5) {
	console.log("REPROVADO")
	console.log("Não emitir certificado")
} else {
	console.log("APROVADO")
	console.log("Emitir certificado")
}
```

Isso daqui não
```javascript
let media = 4

if(media < 5) 
	console.log("REPROVADO")
	console.log("Não emitir certificado")
else // <---  dá erro aqui
	console.log("APROVADO")
	console.log("Emitir certificado")

```

Mas isso aqui sim 
```javascript
let media = 4

if(media < 5) 
	console.log("REPROVADO")
else // <---  dá erro aqui
	console.log("APROVADO")
	console.log("Emitir certificado")

```

```javascript
let media = 4

if(media < 5) 
	console.log("REPROVADO")
else // <---  dá erro aqui
	console.log("APROVADO")
console.log("Emitir certificado")
```
Assim tb funciona mas o último `log()` não faz parte do laço

##### for

```javascript
for(let x = 1; x < 10; x++) {
	console.log(x)
	console.log("node.js)
}
```
- output:
	```powershell
	1
	node.js
	2
	node.js
	3
	node.js
	4
	node.js
	5
	node.js
	6
	node.js
	7
	node.js
	8
	node.js
	9
	node.js
	```

```javascript
for(let x = 1; x < 10; x++) 
	console.log(x)
	console.log("node.js)
```
- output
	```powershell
	1
	2
	3
	4
	5
	6
	7
	8
	9
	node js
	```
	*Isso se deve pq a última linha, ele identa fora do laço `for()` e só considera a primeria*

