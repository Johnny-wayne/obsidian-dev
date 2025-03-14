Apresentar e explorar o paradigma de programação orientado a objeto, seus usos e como ele é aplicado no dia a dia da programação.

#### O que é a POO

A POO é um paradigma de programação, ou seja, corresponde a uma técnica de programação para um fim específico.

Dentro dessa técnica, existem quatro pilares:
- Abstração
- Encapsulamento
- Herança 
- Polimorfismo

**![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdw2BgERJFYQzc87pJaJrufy-JJfFQbTpYTgKuWPd0depfUxLA-zH7RUqTjyXvWomHJV81U07aNtMzMRhmjV9cU-ySY5dKUMaSReiMPetPjKRp7GPgKfGtTmA6ux1XhzO7Am34_E8Tssiomu-essA1X9jJjreuubVuqiJO6gqAYl_2bIe-bFpA=nw?key=64JBISzVS5U7AZqmeTLVGw)**

---
#### Tipos de Paradigmas

Um paradigma nada mais é do que um modelo de técnicas, estruturas e formas de solucionar um problema.

Paradigma de de programação é diferente de linguagem de programação. Uma linguagem de programação implementa um ou mais paradigmas.

###### Paradigmas de programação
- Programação Orientada a Objetos (é o que estamos estudando)
- Programação Estruturada 
- Programação Imperativa
- Programação Procedural
- Programação Orientada a Eventos
- Programação Lógica

E por aí vai...

### POO

##### Abstração

Abstrair um objeto do mundo real para um contexto específico, considerando apenas os atributos importantes.

##### Encapsulamento

O encapsulamento serve para proteger uma classe e definir limites para alteração de suas propriedades. Serve para ocultar seu comportamento e expor somente o necessário.

- `ContaCorrente.cs`
	```C#
	public class ContaCorrente
	    {
	        public ContaCorrente(int numeroConta, decimal saldoInicial)
	        {   
	            NumeroConta = numeroConta;
	            saldo = saldoInicial;
	        }
	        public int NumeroConta { get; set; }
			
			// INVISÍVEL à todos menos à  classe
	        private decimal saldo;
	        
	        public void Sacar(decimal valor)
	        {
	            if (saldo >= valor)
	            {
	                saldo -= valor;
	                Console.WriteLine("Saque realizado com sucesso");
	            }
	            else
	            {
	                Console.WriteLine("Valor desejado é maior que o saldo disponível.");
	            }
	        }
	
	        public void ExibirSaldo()
	        {
	            Console.WriteLine("Seu saldo disponível é: " + saldo);
	        }
	    }
	```
	- `private` 
		- ninguém pode ver, nem alterar a propriedade, a não ser a própria classe

- `Program.cs`
	```C#
	using project3.Models;
	
	ContaCorrente c1 = new ContaCorrente(123, 1000);
	
	c1.ExibirSaldo();
	c1.Sacar(5000);
	c1.ExibirSaldo();
	```

##### Herança

A herança nos permite reutilizar atributos, métodos e comportamentos de uma classe em outras classes. Serve para agrupar objetos que são do mesmo tipo, porém com características diferentes.

- `Pessoa.cs`
	```C#
	public class Pessoa
	{
		public string Nome { get; set; }
		public int Idade { get; set; }
	
		public void Apresentar()
		{
			Console.WriteLine($"Olá, meu nome é {Nome} e tenho {Idade} anos!");
		}
	}
	```


Simplesmente fazendo isso, ele já herda as propriedades e métodos da classe `Pessoa`:

- `Aluno.cs`
	```C#
	public class Aluno : Pessoa
	{
	
	}
	```

- **Notas sobre Herança:**
	- Não é bom ter herança em cascata, porque se a classe avô ou pai é modificada ou excluída, todo o resto desaparece. Evite complexidade do seu código.
	- Não é possível mais de uma herança por vez no C#.

##### Polimorfismo

O polimorfismo vem do grego e significa "muitas formas"

Com o polimorfismo, podemos sobrescrever métodos das classes filhas para que se comportem de maneira diferente e ter sua própria implementação.

Se o método herdado atender as necessidades, beleza, se não, muda saporra pra essa classe em específico aqui, mas mantém o nome

###### Polimorfismo em tempo de execução

Para que possamos sobrescrever o método `Pessoa.Apresentar()`, ou seja, dizer *"O método apresentar não serve mais pra mim, quero fazer da minha própria maneira"*, precisamos declarar que o método pode ser alterado. Fazemos isso com `virtual`.

```C#
public class Pessoa
{
	public string Nome { get; set; }
	public int Idade { get; set; }
	
	public virtual void Apresentar()
	{
		Console.WriteLine($"Olá, meu nome é {Nome} e tenho {Idade} anos!");
	}
}
```

- E aí sobrescrevemos ele usando `override`
	
	- `Professor.cs`
		```C#
		public class Professor : Pessoa
		{
			public decimal Salario { get; set; }
			
			public override void Apresentar() 
			{
				Console.WriteLine($"Olá, meu nome é {Nome}, tenho {Idade} anos, sou um professor e ganho {Salario}");
			}
		}
		```
	
	- `Aluno.cs`
		```C#
		public class Aluno : Pessoa
		{
			public double Nota { get; set; }
			public override void Apresentar()
			{
				Console.WriteLine($"Olá, meu nome é {Nome}, tenho {Idade} anos, e sou um aluno nota {Nota}");
			}
		}
		```


###### Notas sobre Polimorfismo

- **Polimorfismo em tempo de compilação *(Overload / Early Binding)**
	- *Polimorfismo que não dependente de Herança*
	- Nomes iguais, com números de parâmetros diferentes
	
	```C#
	public class Calculadora
	{
		// Se você passar dois argumentos, caí nesse
		public int Somar(int num1, int num2)
		{
			return num1 + num2;
		}
		
		// Se você passar três argumentos, caí nesse
		public int Somar(int num1, int num2, int num3)
		{
			return num1 + num2 + num3;
		}
	}
```

- **Polimorfismo em tempo de Execução *(Override / Late Binding)**
	- *Polimorfismo que dependente de Herança*
	- Nomes iguais, com números de parâmetros diferentes
	
	```C#
	public class Pessoa
	{
		public string Nome { get; set; }
		public int Idade { get; set; }
		public string Email { get; set; }
		
		public virtual void Apresentar()
		{
			Console.WriteLine($"Olá, meu nome é {Nome} e tenho {Idade} anos!");
		}
	}
	
	public class Aluno : Pessoa
	{
		public double Nota { get; set; }
		public override void Apresentar()
		{
			Console.WriteLine($"Olá, meu nome é {Nome}, tenho {Idade} anos, e sou um aluno nota {Nota}");
		}
	}
```


#### Herança - Parte 2
#### Classes Abstratas e Interfaces

Uma classe abstrata tem como objetivo ser exclusivamente um modelo para ser herdado, portanto não pode ser instanciada. Você pode implementar métodos ou deixá-los a cargo de quem herdar.

- Imagem
	![[Pasted image 20240908171138.png]]

##### Classe Abstrata na prática

```C#
public abstract class Conta
{
	protected decimal saldo;
	
	public abstract void Creditar(decimal valor);
	
	public void ExibirSaldo()
	{
		Console.WriteLine("O seu saldo é: " + saldo);
	}
}
```

- Entendendo essa porra
	- `protected`
		- Protege de alterações externas, com exceção de dentro de suas classes filhas.
	- `abstract` 
		- Proíbe instanciar a classe, métodos ou propriedades, permitindo apenas herdar ela.

- `Corrente.cs`
	```C#
	public class Corrente : Conta
	{
		
	}
	```
	 Se fizermos isso aqui, vai dar erro, porque todo método abstrato, precisamos implementar
	
	- Assim não dá pau:
		```C#
		public class Corrente : Conta
		{
			public override void Creditar(decimal valor)
			{
				saldo += valor;
			}
		}
		```
		***Dica:** Se apertar `crtl .` no erro, ele apresenta a opção de implementar todas as classes abstratas*



##### Construtor por Herança

Também podemos definir um Construtor pai para ser herdado pelas classes filhas

```C#
public class Pessoa
{
	// definimos um construtor na classe Pessoa que pede um nome
	public Pessoa(string nome)
	{   
		Nome = nome;
	}

	public string Nome { get; set; }
	public int Idade { get; set; }

	public virtual void Apresentar()
	{
		Console.WriteLine($"Olá, meu nome é {Nome} e tenho {Idade} anos!");
	}
}
```

Mas nas classes `Professor` e `Aluno` que herdam da classe `Pessoa` não temos um construtor, e muito menos passamos o parâmetro `nome`

```C#
public class Aluno : Pessoa
{
	public double Nota { get; set; }
	public override void Apresentar()
	{
		Console.WriteLine($"Olá, meu nome é {Nome}, tenho {Idade} anos, e sou um aluno nota {Nota}");
	}
}

public class Professor : Pessoa
{
	public decimal Salario { get; set; }
	public override void Apresentar() 
	{
		Console.WriteLine($"Olá, meu nome é {Nome}, tenho {Idade} anos, sou um professor e ganho {Salario}");
	}
}
```


Pra consertar, fazemos isso:

```C#
public class Professor : Pessoa
{
	public Professor(string nome) : base(nome)
	{
	
	}
	//mais código...
```

Passamos  o parâmetro `nome` do construtor da classe `Professor` como argumento para o parâmetro `nome` do construtor da classe `Pessoa`, e assim resolvemos o problema.

*Aplicamos isso para todas as classes filhas de `Pessoa`*

---
##### Classe selada

Uma classe selada tem como objetivo de impedir que outras classes façam uma herança dela, ou seja, nenhuma classe pode ser sua derivada. Também existem métodos e propriedades seladas.

###### Classe selada na prática
```C#
public sealed class Professor : Pessoa

public class Diretor : Professor // ---> Error: 'Diretor': cannot derive from sealed type 'Professor'
```

###### Método selado na prática

```C#
public class Professor : Pessoa
{

	public decimal Salario { get; set; }
	public sealed override void Apresentar() 
	{
		Console.WriteLine($"Olá, meu nome é {Nome}, tenho {Idade} anos, sou um professor e ganho {Salario}");
	}
}


public class Diretor : Professor
{
	public override void Apresentar() // <-- Error: 'Diretor.Apresentar()': cannot override inherited member 'Professor.Apresentar()' because it is sealed[CS0239]
	{
		Console.WriteLine("Diretor");
	}
}
```

---
##### Introdução classe Object

A classe `System.Object` é a mãe de todas as classes na hierarquia do .NET

Todas as classes derivam, direta ou indiretamente da classe Object, e ela tem como objetivo prover serviços de baixo nível para suas classes filhas.

Documentação: [Object Class](https://learn.microsoft.com/en-us/dotnet/api/system.object?view=net-8.0)

---
###### Na prática

É como se acontecesse basicamente isso. 
```C#
public class Computador : Object
{

}
// obs: é redundante fazer isso
```

A classe `Object` vem com alguns métodos já, então daria pra fazer isso por exemplo:
```C#
public class Computador
{
	public override string ToString()
	{
		return "Método ToString sobrescrito";          
	}
}
```

---
##### Interfaces

Uma *Interface* é um contrato que pode ser implementado por uma classe. É como se fosse uma classe abstrata, podendo definir métodos abstratos para serem implementados. Assim como uma classe abstrata, uma interface não pode ser instanciada.

- Imagem
	![[Pasted image 20240909204222.png]]
	Toda classe que implementar essa Interface precisará implementar também os métodos dela. Neste caso, com interfaces, o termo certo não é *"herdar"* e sim ***"Implementar"***
	
	- Todo nome de interface começa com `I` como `ICalculadora`

Em C#, não temos o conceito de *herança múltipla* então uma classe não poderia herdar de duas classes ao mesmo tempo. Se eu quiser herdar mais, eu crio uma classe que herda de outra classe.

Com Interfaces, isso é diferente, eu posso ***implementar*** `ICalculadora` e outra interface ao mesmo tempo

Ou seja, basicamente, uma classe abstrata que permite herança múltipla

---
##### Na prática

```C#
public interface ICalculadora
    {
        int Somar(int num1, int num2);
        int Subtrair(int num1, int num2);
        int Multiplicar(int num1, int num2);
        int Dividir(int num1, int num2);
    }
```

- Detalhes:
	- Podemos notar que por convenção usamos o `I` antes do nome da Interface
		
	- Também não temos os acessores `public`, `private` ou `protected` porque subentende-se que ela é pública.
		
	- Só tem a assinatura do método: *o tipo de retorno, o nome e os parâmetros*

Pra ***implementar*** uma Interface, é assim:
```C#
	// Importamos
	using project3.Interfaces;
	
	namespace project3.Models
	{
		// E usamos
	    public class Calculadora : ICalculadora
	    {
	    
		}
```

Mas vai dar erro, porque não implementamos os métodos da Interface ainda. Ela é um contrato, ou seja, tudo que ela pedir para implementar, tem que implementar. 

Mas aí é só implementar tb né:
```C#
	public class Calculadora : ICalculadora
	{
		public int Dividir(int num1, int num2)
		{
			return num1 / num2;
		}
	
		public int Multiplicar(int num1, int num2)
		{
			return num1 * num2;
		}
	
		public int Somar(int num1, int num2)
		{
			return num1 + num2;
		}
	
		public int Subtrair(int num1, int num2)
		{
			return num1 = num2;
		}
	}
```

> "*`Calculadora` implementa a interface `ICalculadora`*"

##### Método padrão na Interface

```C#
	public interface ICalculadora
	{
		int Somar(int num1, int num2);
		int Subtrair(int num1, int num2);
		int Multiplicar(int num1, int num2);
		int Dividir(int num1, int num2)
		{
			return num1 / num2;
		}
	}
	
	public class Calculadora : ICalculadora
    {
		// Não vai dar erro
        public int Multiplicar(int num1, int num2)
        {
            return num1 * num2;
        }
		
        public int Somar(int num1, int num2)
        {
            return num1 + num2;
        }
		
        public int Subtrair(int num1, int num2)
        {
            return num1 = num2;
        }
    }
```

- Não vai dar erro, porque implementamos um comportamento padrão para o método Dividir da interface, podemos implementar nosso próprio método dentro da classe Calculadora