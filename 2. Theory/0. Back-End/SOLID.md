==*Não sei em qual linguagem foram escritas as classes*==

***S.O.L.I.D***

**S** - Single Responsibility Principle
**O** - Open-Closed Principle
**L** - Liskov Substitution Principle
**I** - Interface Segregation Principle
**D** - Dependency Inversion Principle

---
#### S - Single Responsibility Principle (S.R.P)

Uma classe deve ter apenas uma funcionalidade dentro do software, ser especializada em apenas um assunto.

As classes *"faz-de-tudo"* são chamadas de *"god classes"*, elas dificultam e muito a manutenção do código.  

- Exemplo:
	```php
	Class Order {
		
		public function calculateTotalSum() {/*...*/}
		public function getItems() {/*...*/}
		public function getItemCount() {/*...*/}
		public function addItem($item) {/*...*/}
		public function calculateTotalSum($item) {/*...*/}
		
		public function printOrder() {/*...*/}
		public function showOrder() {/*...*/}
		
		public function load() {/*...*/}
		public function save() {/*...*/}
		public function update() {/*...*/}
		public function delete() {/*...*/}
	}
	```
	Essa classe viola o Princípio ***SRP***, pois lida não somente com as informações do pedido, mas também pela exibição e manipulação dos dados.

Esse problema gera:
- Falta de coesão
	- Classe assume responsabilidades que não são as suas
- Auto-acoplamento
	- Mais responsabilidades geram maior níveis de independências, o que deixa o sistema engessado e frágil pra alterações
- Dificuldades com Testes Automatizados
	- Tornando difícil de bocar esses tipos de classes
- Tornando difícil de reaproveitar o código

- Assim é como a classe deveria ficar:
```php
class Order {
	public function calculateTotalSum() {/*...*/}
	public function getItems() {/*...*/}
	public function getItemCount() {/*...*/}
	public function addItem($item) {/*...*/}
	public function calculateTotalSum($item) {/*...*/}
}

class OrderRepository {
	public function load() {/*...*/}
	public function save() {/*...*/}
	public function update() {/*...*/}
	public function delete() {/*...*/}
}

class OrderViewer {
	public function printOrder() {/*...*/}
	public function showOrder() {/*...*/}
}
```

***Obs:*** Lembre-se que este princípio também engloba métodos e funções.

---
#### O - Open-Closed Principle (OCP)

Objetos e entidades devem estar abertos para extensão, mas fechados para modificação.

Eis aqui um exemplo de um software de RH:
```php
class ContratoClt {
	public function salario() {/*...*/}
}

class Estagio {
	public function bolsaAuxilio() {/*...*/}
}

class FolhaDePagamento {
	protected $saldo;
	
	public function calcular( $contrato ) {
	
		if ( $contrato instanceof ContratoClt ) {
			$this->saldo = $contrato->salario();
		} 
		
		else if ( $contrato instanceof Estagio ) {
			$this->saldo = $contrato->bolsaAuxilio();
		}
		
	}
}
```

Aqui tem um porém. Imagine que essa empresa, agora decida contratar por PJ, criando uma nova função. Agora seria necessário modificar a classe `FolhaDePagamento`, talvez adicionando um novo `if()`, ferindo o princípio ***Open-Closed***, de permitir extender, mas não alterar. 

Ferir esse princípio é ruim porque corremos o risco de criar bugs em um código que já funcionava.

Neste caso, a solução seria:
> *"separe o comportamento extensível, a partir de uma Interface, inverta as dependências."*

Abstrair o contexto em uma interface.

Ficaria assim do jeito certo:
```php
interface Remuneravel { 
	public function remuneravel();
}

class ContratoClt implements Remuneravel {
	public function remuneracao() {/*...*/}
}

class ContratoPj implements Remuneravel {
	public function remuneracao() {/*...*/}
}

class Estagio implements Remuneravel {
	public function remuneracao() {/*...*/}
}

class FolhaDePagamento {
	protected $saldo;
	
	public function calcular( Remuneravel $contrato ) {
		$this->saldo = $contrato->remuneracao();
	}
}

```

---
#### L - Liskov Substitution Principle (LSP)

Uma classe derivada deve ser substituível por sua classe base

```php
class A {
	public function getNome() {
		echo 'Meu nome é A';
	}
}

class B extends A {
	public function getNome() {
		echo 'Meu nome é B';
	}
}

$objeto1 = new A;
$objeto2 = new B;

function imprimeNome( A $objeto ) {
	return $objeto->getNome();
}

imprimeNome($objeto1); //Meu nome é A
imprimeNome($objeto2); //Meu nome é B
```

Basicamente é usar polimorfismo, sem mexer no método da classe base. Pelo menos, foi o que entendi.

---
#### I - Interface Segregation Principle (ISP)

Onde uma classe não deve ser forçada a implementar interfaces e métodos que não vai usar. Basicamente, esse princípio diz que é melhor ter várias interfaces especificas do que ter uma interface genérica.

Imagine que temos um jogo de bichos, que tem essas aves.
```php
interface Aves {
	public function setLocalizacao( $longitude, $latitude );
	public function setAltitude( $altitude );
	public function renderizar();
}

class Papagaio implements Aves { 
	public function setLocalizacao( $longitude, $latitude ) {/*...*/}
	public function setAltitude( $altitude ) {/*...*/}
	public function renderizar() {/*...*/}
}

class Pinguim implements Aves {
	public function setLocalizacao( $longitude, $latitude ) {/*...*/}
	public function setAltitude( $altitude ) {
		//Não faz nada, pinguins não voam!
	}
	public function renderizar() {/*...*/}
}
```
Aqui estamos violando tanto o ISP quanto LSP. 
- Violamos o ISP por ter que definir um método dentro da classe Pinguim que não faz nada. E por alterar o comportamento

O jeito que é criar uma nova Interface com valores diferentes:
```php
interface Aves {
	public function setLocalizacao( $longitude, $latitude );
	public function renderizar();
}

interface AvesQueVoam extends Aves {
	public function setAltitude($altitude);
}

class Papagaio implements AvesQueVoam { 
	public function setLocalizacao( $longitude, $latitude ) {/*...*/}
	public function setAltitude( $altitude ) {/*...*/}
	public function renderizar() {/*...*/}
}

class Pinguim implements Aves {
	public function setLocalizacao( $longitude, $latitude ) {/*...*/}
	public function renderizar() {/*...*/}
}
```


---
#### D - Dependency Inversion Principle (DIP)

Devemos depender de abstrações e não de implementações

> Módulos de alto nível, não devem depender de módulos de baixo nível. Ambos devem depender de abstração. E abstrações não devem depender de detalhes, detalhes devem depender de abstrações.

código de recuperação de senha:
```php
use MySQLConnection;

class PasswordReminder {
	private $dbConnection;
	
	public function __construct() {
		$this->dbConnection = new MySQLConnection();
	}
	
	//faz alguma coisa
}
```

Parece ser meio avançado aqui.

Eles falam que temos um "alto acoplamento" nesse código pelo fato de que caso precisemos implementar essa classe em outro sistema, precisaríamos levar a classe `MySQLConnection` junto. 

Como resolvemos esse problema de acoplamento?
```php
use MySQLConnection

class PasswordReminder {
	private $dbConnection;
	
	public function __construct( MySQLConnection $dbConnection ) { 
		$this->dbConnection = $dbConnection;
	}
	
	//faz alguma coisa
}
```
Essa sintaxe tb não ajuda né. 

Mas pelo que explicaram, o problema foi resolvido por tirar a responsabilidade da classe de criar uma instância de `MySQLConnection` por transformar ele em uma dependência por meio do construtor, que deve ser injetada via método construtor.

Mas ainda devemos melhorar nível de acoplamento desse código, porque ele ainda viola o princípio de *Inversão de dependência - DIP*, e também, o princípio *Open-Closed - OCP*.

- Ele viola o *OCP* porque, caso precisemos usar outro banco de dados, além do MySQL, precisaríamos mexer em código já funcional.

- Ele viola o *DIP* porque, a nossa classe `PasswordReminder` depende da nossa classe `MySQLConnection`, sendo assim, a classe `PasswordReminder` é o módulo de alto nível e o `MySQLConnection` é o módulo de baixo nível, que por sua vez, é uma implementação e não uma abstração.

Agora iremos refatorar programando para uma interface e não para uma implementação:
```php
interface DBConnectionInterface {
	public function connect();
}

class MySQLConnection implements DBConnectionInterface {
	public function connect() {/*...*/}
}

class OracleConnection implements DBConnectionInterface {
	public function connect() {/*...*/}
}

class SQLServer implements DBConnectionInterface {
	public function connect() {/*...*/}
}

class PasswordReminder {
	private $dbConnection;
	
	public function __construct( DBConnectionInterface $dbConnection ) {
		$this->dbConnection = $dbConnection;
	}
	
	//Faz alguma coisa
}
```
Esse é um código perfeito, não estamos violando mais nada. 

- Isso se deve ao fato das classes estarem desacopladas e estarmos favorecendo a reusabilidade do código.