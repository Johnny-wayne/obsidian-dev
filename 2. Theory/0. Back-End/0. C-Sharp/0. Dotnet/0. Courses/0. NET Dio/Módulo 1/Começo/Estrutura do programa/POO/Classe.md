
### Classe
Convenção: Todo nome de classe, começa maiúsculo
`PessoaFisica`

> [!tip] property
> Se você escrever `prop` e apertar `Tab` ele completa pra ti e aparece isso aqui:
> `public int MyProperty { get; set; }`

Classe inicial `Desktop/DioNet/Models/Pessoa.cs`
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

namespace NetDio.Models
{
    public class Pessoa
    {
        public string Nome { get; set; }
        public int Age { get; set; }
  
        public void Apresentar()
        {
            Console.WriteLine($"Olá, meu nome é {Nome}, e minha idade é {Idade}")
        }
    }
}
```

###### Entendendo esta porra:

- `public class Pessoa`
	```C#
	public class Pessoa
	```
	É uma classe porque tem `class` escrito
	
- `{ get; set; }`
	```C#
	public string Nome { get; set; }
	```
	
	- A parte `get` representa a ação de quando o elemento está sendo "pego", como esse exemplo:
		```C#
		Console.WriteLine($"Olá, meu nome é {Nome}, e minha idade é {Idade}")
		```
		
	- E a parte `set` quando o elemento é definido
		```C#
		Nome = "Gabriel"; //o = aqui representa o `set`
		```
	
- `namespace ExemploFundamentos.Models`
	```C#
	namespace NetDio.Models {}
	```
	- É uma organização de suas classes
		- Elas representam um caminho lógico pra identificar classes que estejam no mesmo domínio
		- Todas as `Models` colocaremos com esse mesmo `namespace` para sabermos depois onde elas estão.
		- Neste caso, `NetDio` representa a pasta que estamos salvando todo esse programa, e `Models` a pasta ***Models*** dentro dela
		- Lembrando que não é o endereço físico, apenas o virtual. 
			- Então daria pra colocar: `namespace Pilimpimpom.baguete`
			- Não temos nem a pasta *"pilimpimpom"* e nem a *"baguete"* 
		- ==Mas é uma boa prática fazer assim==
	- É interessante, que caso criássemos um classe `conta_corrente` por exemplo, colocássemos algo como:
		- `namespace NetDio.Models.Contas`
		- E dentro dela, colocássemos as classes `conta_corrente`, `conta_poupança` e etc. Pra nos organizarmos.
	
- Palavras reservadas
	- São palavras que não podemos usar porque o próprio C# usa, por exemplo:
		- `public`
		- `class`
		- `void`
		- `get`
		- `set` 
		- `namespace`
		- etc.
	- Isso dá pau, por exemplo:
		  - `string teste = public;`
		  - `string teste = void`
	- Mas tem exceções:
		- `@class = "teste";`
		- Quando usamos o "@", isso indica ao C# que sabemos que é uma palavra reservada, mas queremos usar mesmo assim.
		- Mas não é legal de fazer não


### Classe Calculadora


- Tudo isso aqui, a gente basicamente já sabe 
	```C#
	public class Calculadora 
	{
		public void Somar(int x, int y)
		{
			Console.WriteLine($"{x} + {y} = {x + y}");
		}
		public void Subtrair(int x, int y)
		{
			Console.WriteLine($"{x} - {y} = {x - y}");
		}
		public void Multiplicar(int x, int y)
		{
			Console.WriteLine($"{x} x {y} = {x * y}");
		}
		public void Dividir(int x, int y)
		{
			Console.WriteLine($"{x} / {y} = {x / y}");
		}
		
	}
	```
	
	```C#
	Calculadora calc = new Calculadora();
	
	calc.Somar(10, 30);
	calc.Subtrair(10, 30);
	calc.Multiplicar(10, 30);
	calc.Dividir(10, 30);
	```
- Classe `Math`
	```C#
	public void Potencia(int x, int y)
	{
		double pot = Math.Pow(x, y);
		Console.WriteLine($"{x}^{y} = {pot}");
	}
	```
	
	- Dentro da classe `Math` temos diversas operações matemáticas, tais como Potências, Logaritmos, Sin, etc.

----

- Funções Trigonométricas
	```C#
	public void Seno(double angulo)
	{
		double radiano = angulo * Math.PI / 180;
		double seno = Math.Sin(radiano);
		Console.WriteLine($"Seno de {angulo}* = {Math.Round(seno, 4)}");
	}
	public void Coseno(double angulo)
	{
		double radiano = angulo * Math.PI / 180;
		double coseno = Math.Cos(radiano);
		Console.WriteLine($"Coseno de {angulo}* = {Math.Round(coseno, 4)}");
	}
	public void Tangente(double angulo)
	{
		double radiano = angulo * Math.PI / 180;
		double tangente = Math.Tan(radiano);
		Console.WriteLine($"Tangente de {angulo}* = {Math.Round(tangente, 4)}");
	}
	```
	- `Math.Round()` arredonda o número
	- Usa o Math. e explora e pesquisae, mó rolê aprender Trigonometria agora

---
- Calculando raiz quadrada
	```C#
	public void RaizQuadrada(double x)
	{
		double raiz = Math.Sqrt(x);
		Console.WriteLine($"Raiz quadrada de {x} = {Math.Round(raiz, 4)}");
	}
	```

---
### Usando a classe Pessoa

Aula anterior: [[Usando namespaces]]

Agora que nós instanciamos a pessoa.
```C#
using NetDio.Models;

Pessoa pessoa1 = new Pessoa();
```

- Entendendo essa porra:
	- `Pessoa` - Tipo
	- `pessoa1` - nome da varíavel
	- `new` - novo
	- `Pessoa()` - Classe

---
- O que seria Instanciar?
	- No ponto de vista que a Classe é uma blueprint
	- `pessoa1` é o "produto" criado a partir da blueprint `Pessoa()`
	- Ou seja, é a instância
		- Dá pra fazer várias instâncias de uma mesma blueprint (classe) que são independentes umas das outras, cada uma com seus valores.
	
	Todas as instâncias possuem métodos padrões do C#, porque são do tipo `Object`
	- Ex:
		- `pessoa1.getHashCode` porque foi definido no C# que `Object.getHashCode()`
		- `Object: {getHashCode(): { CódigoAleatório }}`
		- Ou algo assim

Ex de uso:
```C#
using NetDio.Models;

Pessoa pessoa1 = new Pessoa();

pessoa1.Nome = "Buta";
pessoa1.Idade = 26;
pessoa1.Apresentar();
```

- Output
	```bash
	Olá, meu nome é Buta, e minha idade é 26
	```

