###### O que é o TypeScript?

- TypeScript é um *superset* para a linguagem JavaScript;
- Ou seja, adiciona funções ao JavaScript, como a *declaração de tipos* de variável;
- Pode ser utilizada com frameworks/libs, como: **Express** e **React**;
- Precisa ser *compilado em JavaScript*, ou seja, não executamos TS;
- Desenvolvido e mantido pela Microsoft;
	- Ou seja, vai ter longa vida e vai ser continuado.

---

###### Por que TypeScript?

- Adiciona *confiabilidade* ao programa (tipos);
- Provê novas funcionalidades a JS, como **[[Interfaces]]**;
- Com TS podemos verificar os erros antes da execução do código, ou seja, no desenvolvimento;
- Deixa JavaScript mais explícito, diminuindo a quantidade de bugs;
- Por estes e outros motivos perdemos menos tempo com debug;

---

###### Instalando o TypeScript

- Para instalar o TypeScript vamos utilizar o **npm**
- O nome do pacote é TypeScript
- E vamos adicionar de forma global com a `flag -g`;
- A partir da instalação temos como executar/compilar TS em qualquer local da nossa máquina, com o comando `tsc`.

Ele vai no site do Node, instala o NodeJS
-  depois ele abre o terminal integrado e coloca:
	  `node -v`
E depois:
	  `npm -v`
Depois de verificar a instalação desses dois na máquina, ele coloca o comando:
	`npm i -g typescript`
Graças a instalação global do TypeScript com o -g, ele fica disponível no terminal, e pra verificar se a instalação tá feita, você usa:
	`tsc -v`
	

---
##### Começo

No começo de um projeto TS, normalmente se começa da seguinte forma:

- Criação das pastas de código, sendo:
	- `dist` (de distribuição, para poder hospedar em algum lugar)
	- `src` (de source, aonde vamos desenvolver nosso projeto)

---
###### Explicação
Imagine que você está construindo uma casa. Antes de começar a erguer as paredes e pintar as salas, você precisa de um plano, certo? Um projeto arquitetônico que detalha como a casa será construída, onde ficarão os quartos, a cozinha, etc.

No *desenvolvimento de software*, é mais ou menos a mesma coisa. Antes de começar a escrever o código que fará a sua aplicação funcionar, você precisa de uma ==estrutura básica==, um esqueleto, para organizar tudo. E é aí que entram as pastas `dist` e `src`.

1. **`src` (Source)**: ==Esta é a pasta onde você vai realmente trabalhar==. É onde você escreve o *código-fonte* do seu projeto. Aqui você coloca todos os arquivos TypeScript (ou JavaScript, se preferir) que definem como a sua aplicação vai funcionar. É onde você escreve as suas classes, funções, variáveis e tudo mais que compõe a lógica do seu programa.
    
	Imagine a pasta `src` como a planta da sua casa. É onde você coloca todos os detalhes sobre como a aplicação será construída.
	
2. **`dist` (Distribution)**: Esta é a pasta onde o ==código pronto para ser executado== é gerado. Quando você escreve código TypeScript, ele precisa ser traduzido para JavaScript para que os navegadores e outros ambientes de execução possam entendê-lo. A pasta `dist` é ==onde esse código JavaScript é colocado depois que o TypeScript é compilado==. É como se fosse a casa construída, pronta para ser habitada.
    
    Comparando com a construção da casa, a pasta `dist` seria o resultado final, a casa pronta para ser ocupada. É onde está o código que pode ser executado pelos usuários ou pelo servidor.
    

Em resumo, `src` é onde você escreve o código-fonte da sua aplicação, enquanto `dist` é onde o código pronto para ser executado é armazenado após a compilação. Essas pastas são separadas para manter o seu ambiente de desenvolvimento organizado e facilitar a distribuição da sua aplicação quando estiver pronta.

---

Dentro da pasta `dist`:
==index.html==
```html
<!DOCTYPE html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Curso de TypeScript</title>
    <script src="js/index.js" defer></script>
</head>
<body>
</body>
</html>
```

O atributo `defer`, permite que o HTML seja carregado antes do JavaScript.

Dentro da pasta `src`:
==index.ts==
```ts

```

Basicamente, todo projeto TypeScript, necessita de um arquivo de configuração para gente poder estabelecer algumas mudanças nele, se assim precisar, e para dizer que aqui é um projeto TypeScript.

E isso pode ser feito a partir do comando:
`tsc --init`

ele retorna dentro do terminal (do maluco retornou):
```powershell
Created a new tsconfig.json with:

	target: es2016
	module: commonjs
	strict: true
	esModeuleInterop: true
	skipLibCheck: true
	forceConsistentCasingInFileNames: true

You can learn more at https://aka.ms/tsconfig.json
```

---
No *arquivo de configuração* temos algumas coisa, como:

- De compilação
	`"compilerOptions": {`
	- Versão do JavaScript está sendo compilado
		- `"target": "es2026"`
	- O diretório base da aplicação
		- `"rootDir": "./"` 
		- Aqui estava comentado, mas posteriormente ele muda para:
			- `"rootDir": "./src"`
			- Já que é a pasta que a gente tá desenvolvendo o código
	- Diretório de saída, que seria o diretório de distribuição ou de deploy
		- Que estava comentado como:
		- `"outDir": "./"`
			- Mas ele mudou para: 
			- `"outDir": "./dist/js/"`
				- Por ser a pasta que compila JS especificada no HTML,  como: `"js/index/js"` 

---
Na maior parte das vezes a gente pode escrever em JavaScript, sem se preocupar com o TypeScript.

Se vc digitar `tsc` no terminal, ele compila automaticamente pra JS o arquivo de TypeScript, aonde especificamos no `tsConfig`. Ou seja, cria-se uma pasta chamada `js` com um arquivo chamado `index.js`. No final o caminho fica:
	`dist/js/index.js`

---

Então o arquivo de TS que estava assim:
```typeScript
//string, boolean, number...
let x: number = 10;

x = 16;

console.log(x);
```

vai ficar assim:
```JS
"use strict";
//string, boolean, number...
let x: number = 10;
x = 16;
console.log(x);
```

Nesse caso, imprimiu exatamente da mesma forma. Mas algumas funcionalidade extras do TS, às vezes, serão impressas de outra forma. Outras vezes, nem serão colocadas, porque são importantes apenas no ambiente de desenvolvimento.

Temos que prestar bastante atenção para quem estamos criando esse código.

Caso estejamos criando para um navegador, nós podemos mudar a versão do JavaScript no `tsConfig`, para uma mais antiga como `"target": "ES3";`, sendo o mais indicado nesse caso.

Também podemos colocar versões mais recentes do JS, como: `"target": "esnext";`

--- 
Uma coisa importante também, à nível do computador, é a compilação automática.

Então digitamos `tsc -w` no terminal integrado

E retorna isso no terminal dele: 
```terminal
starting compilation in watch mode...

Found 0 erros. Watching for file changes
```
Agora qualquer alteração no código TS, vai ser refletida no código JS, diretamente.

Ele utiliza o ==Live Server== para gerar um servidor embutido. Não entendi muito bem, mas na internet diz:

> [!quote] Live Server
> O Live Server é uma extensão para o Visual Studio Code que **cria um servidor local para hospedar seu projeto e atualizar automaticamente a página quando você faz alterações no código**. Em um servidor local, como o Live Server, o JavaScript pode ser executado sem problemas.
> - Alura

----
##### Inferencia x annotation
Essa é outra regra muito importante do TS.
São dois modos de definir valores com tipos no TS.

==inferencia==
```ts
let y = 12; 
y = "teste"; //aqui vai dar pau, pq y foi definido como tipo number, por inferencia, mesmo com o let
```

==annotation==
```ts
let x: number = 12; 
x = "teste"; //aqui vai dar pau, pq x foi definido como tipo number, por annotation
```

---
#### Tipos

- Básicos
	- string
	- number
	- boolean
	

 - Array: `const myNumbers: number[] = [1, 2, 3];`

---

- Tuplas/Tuples: 
```ts
let myTuple: [number, string, string[]]

myTuple = [5, "teste", ["a", "b"]] //correto
myTuple = [true, false, true]      //errado
```


---

- object literals -> `{prop: value}`
	em outras linguagens é chamado de *array de chaves e valores*, aonde a gente 
	tem como pegar um valor pelo nome da sua chave.
	
```ts
const user: {name: string, age: number} = {
	firstName: "Pedro" //errado
	name: "Pedro" //correto
	
	//Mas ainda não deixa, dá erro, porque falta o age
	
	age: 18
}

console.log(user);
//retorna {name: 'Pedro', age: 18}
```


---

- Any - aceita qualquer tipo de dado
```ts
let a: any = 0;

a = "teste"; // ele vai aceitando todos esses valores
a = true;
a = [];

//o ruim, é que vai contra a filosofia do TypeScript, de tipar
//ou seja, é uma má prática
```


---

###### Union Type
Solução para o `any`

```ts
let id: string | number = 10; //o nome dessa barra vertical é pipe

id = 200;             //certo
id = "13oj9jijedfsd"; //certo

id = true;            //errado
id = [];              //errado
```


--- 
##### Criando tipos
Type alias -> determinar o nome de um tipo

```ts
type myIdType = number | string;

const userId: myIdType = 10;
const productId: myIdType = "00001";
const shirId: myIdType = 123;
```

Pode colocar quantos alias quiser, como:
`type myIdType = number | string | array;`

---
###### Enum - outro tipo de dado
Enumera uma coleção para tratar dados mais complexos de formas mais simples.

Ex: tamanho de roupas (size: Médio, size: Pequeno)
```ts
enum Size {
	P = "Pequeno",
	M = "Médio",
	G = "Grande"
}

const camisa = {
	name: "Camisa gola V",
	size: Size.G,
};

console.log(camisa);
```
Também é usado em React para algumas situações.

---
###### Literal Types
Determinar um valor como um tipo

ex: 
```ts
let teste: "algumvalor";

teste = "outrovalor" //dá erro
teste = "algumvalor" //dá certo
```

Normalmente é utilizado com `null`
```ts
let teste: "autenticado" | null;

teste = "autenticado";
teste = null;
```
Inicia como null, e quando logar, muda pra autenticado

---
#### Funções

```ts
function sum(a, b) {
	return a + b;
}
```
Má pratica, porque os parâmetros "a" e "b", estão definidos como "any" por inferencia

```ts
function sum(a: number, b: number) {
	return a + b;
}
```

- Tipando o retorno
```ts
function sayHelloTo(name: string): string {
	return `Hello ${name}`;
}

console.log(sayHelloTo("Matheus"));
```

- void - tipo de função que não retorna nada
```ts
function logger(msg: string): void {
	console.log(msg);
}

logger("Teste!");
```

---
##### Interfaces
Padronizam algo, para que possamos reutilizar como tipo.
Temos vários modelos. Basicamente podemos tipar um objeto.

```ts
interface MathFunctionParams {
	n1: number,
	n2: number
}

function sumNumbers(nums: MathFunctionParams) {
	return nums.n1 + nums.n2;
}

console.log(sumNumbers({ n1: 1, n2 :2 }));

function multiplyNumbers(nums: MathFunctionParams) {
	return nums.n1 * nums.n2; 
	//assim, reaproveitamos o tipo em várias funções
}

const someNumbers:MathFunctionParams = {
	n1: 5,
	n2: 10
}

console.log(multiplyNumbers(someNumbers));

```

---

##### Narrowing - checagem de tipos
Recurso um pouco mais teórico. Existem muitos tipos.

exemplo1:
```ts
function greeting(name: string, greet?: string): void {
	if (greet) {
		console.log(`Olá ${greet} ${name}`);
		return;
	}
	console.log(`Olá ${name}`);
}

greeting("José");
greeting("Pedro", "Sir");

```

exemplo2 - typeOf
```ts
function doSomething(info: number | boolean) {
	if(typeOf info === "number") {
		console.log(`O número é ${info}`
		return)
	}
	console.log("Não foi passado um número")
}
```

---
##### Generics
Um recurso bem amplo, um pouco mais complexo do que apresentado.
 
Mas basicamente, o tipo de dado pra mim não importa, eu quero executar uma função, que ela trabalhe com aquele tipo de dado, mas ele pode ser qualquer um, dá pra você restringir isso, mas normalmente os genéricos são usados para qualquer coisa

Normalmente são usados `<T>` ou `<U>` para remeter à genéricos
```ts
function showArrayItems<T>()
```

```ts
function showArrayItems<u>()
```

Uma função que recebe um array, mas que seja de qualquer tipo, uma array *genérico*
```ts
function showArrayItems<T>(arr: T[]) {
	arr.forEach((item) => {
		console.log(`ITEM: ${item}`)
	})
}

const a1 = [1, 2, 3]
const a2 = ["a", "b", "c"]

showArraysItems(a1);
showArraysItems(a2);
```
Essa é uma forma de ser mais específico que o `any` e contorná-lo

---
##### Classes
Entrando um pouco em POO

Aqui o TS reclama que o tipo está declarado como `any`
```ts
class User {
	name;
	role;
	isApproved;
}
```

Agora ele reclama que não possui um inicializador
```ts
class User {
	name: string;
	role;
	isApproved;
}
```

Para que não acha repetição de código, declaramos os tipos, dentro do constructor, do inicializador
```ts
class User {
	name;
	role;
	isApproved;
	
	constructor(name: string, role: string, isApproved: boolean) {
		//Aí pra conectar eles a gente usa o this =
		this.name = name;
		this.role = role;
		this.isApproved = isApproved;
	}
}

const zeca = new User("Zéca", "Admin", true);

console.log(zeca);
```

Também dá pra colocarmos métodos.
```ts
class User {
	name;
	role;
	isApproved;
	
	constructor(name: string, role: string, isApproved: boolean) {
		//Aí pra conectar eles a gente usa o this =
		this.name = name;
		this.role = role;
		this.isApproved = isApproved;
	}
	
	showUserNAme() {
		console.log(`O nome do usuário é ${this.name}`)
	}
	
	//tratamos os métodos como se fossem funções, então podemos colocar void por exemplo
	showUserRole(canShow: boolean): void {
		if(canShow) {
			console.log(`Idade do usuário é: ${this.role}`)
			return
		}
		console.log("Informação restrita)
	}
}

const zeca = new User("Zéca", "Admin", true);

console.log(zeca);

zeca.showUserName();

zeca.showUserRole(false);
```

---
##### Interfaces em classes
É o mais core da POO clássica

Aonde temos uma interface que dita como uma classe vai se comportar, isso pode ajudar quando um projeto tem classes muito parecidas.
```ts
// para que consigamos identificar que é uma interface, nós colocamos I antes
interface IVehicle {
	brand: string;
	showBrand(): void;
}

class Car implements IVehicle {
	brand
	wheels
	
	constructor(brand: string, wheels: number) {
		this.brand = brand
		this.wheels = wheels
	}
	
	showBrand(): void {
		console.log(`A marca do carro é: ${this.brand}`)
	}
	
}

const fusca = new Car("VW", 4)

fusca.showBrand();
```

A interface ajuda a criarmos modelos de código entre as classes para padronizarmos melhor nosso sistema.

---
###### Herança
Outra coisa de POO

Aqui vai herdar tudo de `Car`, quando herdamos, não precisamos aplicar a Interface novamente, a Interface é aplicada somente na classe pai.
```ts
class SuperCar extends Car {
	engine
	
	constructor(brand: string, wheels: number, engine: number) {
		//método especial dos construtores
		super(brand, wheels);
		this.engine = engine;
	}
}

const a4 = new SuperCar("Audi", 4, 2.0);

console.log(a4);

a4.showBRand();

//retorna no log

//SuperCar {brand: "Audi", wheels: 4, engine: 2}
//A marca do carro é: Audi
```

---
###### Decorators
Recurso exclusivo TypeScript, usado para validação de dados.
Evita Observável.

Pra usar os *Decorators*, precisamos ir lá no` tsconfig.json`

```ts
class Person {
	name
	
	constructor(name: string) {
		this.name = name;
	}
}

const sam = new Person("Sam");

console.log(sam);
```

Imagine que automaticamente me gere um `id` e uma `data de criação` desse cara, desse usuário desse `Person`.

Então vamos criar uma função. Todo decorator também precisa retornar uma outra função. Que contém as informações que vamos alterar na classe base
```ts
function BaseParamters() {

	return function() {
		
	}

```
Aqui (`return function()`) vamos trabalhar com o construtor, então precisamos fazer com que possamos trabalhar com qualquer tipo de argumento, pois vamos ter classes diferentes umas das outras.

Então usamos um generic (meio complexo), pra isso
```ts
function BaseParamters() {
	
	return function <T extends {new (...args: any[]): {}}>(constructor: T) {
		return class extends constructor {
			id = Math.random();
			createdAt = new Date();
		};
	};
}
```

Aí fica assim:

==constructor decorator==
```ts
function BaseParameters() {
	
	return function <T extends {new (...args: any[]): {}}>(constructor: T) {
		return class extends constructor {
			id = Math.random();
			createdAt = new Date();
		};
	};
}

@BaseParameters()
class Person {
	name
	
	constructor(name: string) {
		this.name = name;
	}
}

const sam = new Person("Sam");

console.log(sam);

```

Existem vários tipos de decorators, alguns talvez sejam aplicados um pouco diferentes.

---
