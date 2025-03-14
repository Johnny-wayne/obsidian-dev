
### Tuplas
*Tuplas fornece sintaxe concisa para agrupar vários elementos de dados em uma estrutura de dados leve.*

Basicamente, é esta porra:
```C#
	(int, string, string) tupla = (0, "J", "W");
```

##### Outras Sintaxes

- Exemplo1
	```C#
		(int Id, string Nome, string Sobrenome, decimal Altura) Exemplo1 = (0, "J", "W", 1.80M);
		
		Console.WriteLine($"Id: {Exemplo1.Id}, Nome: {Exemplo1.Nome}, Sobrenome: {Exemplo1.Sobrenome}, Altura: {Exemplo1.Altura}");
	```
	
	- Também funciona assim:
		```C#
		(int Id, string Nome, string Sobrenome, decimal Altura) Exemplo1 = (0, "J", "W", 1.80M);
		
		Console.WriteLine($"Id: {Exemplo1.Item1}, Nome: {Exemplo1.Item2}, Sobrenome: {Exemplo1.Item3}, Altura: {Exemplo1.Item4}");
		```
	
- Exemplo2
	```C#
	ValueTuple<int, string, string, decimal> Exemplo2 = (2, "b", "string", 1.90M);
	
	Console.WriteLine($"Id: {Exemplo2.Item1}, Nome: {Exemplo2.Item2}, Sobrenome: {Exemplo2.Item3}, Altura: {Exemplo2.Item4}");
	```
	
- Exemplo3
	```C#
	var Exemplo3 = Tuple.Create(4, "2", 24, 1.90M);
	
	Console.WriteLine($"Id: {Exemplo3.Item1}, Nome: {Exemplo3.Item2}, Sobrenome: {Exemplo3.Item3}, Altura: {Exemplo3.Item4}");
	```
	Não precisamos passar um tipo aqui, ele já determina.

Os *Exemplos 2 e 3*, não possuem a capacidade de passar nome aos campos, como `Id, Nome, Sobrenome, Altura`, etc.

O mais recomendado, é a primeira forma, do *Exemplo1*.

##### Tupla em métodos

> [!write] Contexto
> Precisamos criar um método chamado `LerAquivo()` na nova classe `LeituraArquivo`. Que retorne se conseguiu ou não, as linhas, e o número das linhas. Ou seja uma tupla com `bool, string[], int`

- Esse foi o jeito que tentei, e é praticamente a mesma coisa.
	```C#
	public ValueTuple<bool, string[], int> LerArquivo(string caminho)
	{
		string[] linhas = File.ReadAllLines(caminho);
		
		return (true, linhas, linhas.Length);
	}
	```
	
	```output
	(True, System.String[], 4)
	```

O jeito "certo", é esse:
```C#
public (bool Sucesso, string[] Linhas, int QtdLinhas) LerArquivo(string caminho)
{
	try
	{
		string[] linhas = File.ReadAllLines(caminho);
		return (true, linhas, linhas.Count());
	}
	catch (Exception)
	{
		return (false, new string[0], 0);
	}
}
```

`Program.cs`
```C#
LeituraArquivo Leitura = new LeituraArquivo();

var (sucesso, linhasArquivo, quantidadeLinhas) = Leitura.LerArquivo("Arquivos/arquivo.txt");

if (sucesso)
{
    Console.WriteLine("Quantidade linhas do arquivo: " + quantidadeLinhas);
    foreach(string linha in linhasArquivo)
    {
        Console.WriteLine(linha);
    }
}
else
{
    Console.WriteLine("Não foi possível ler o arquivo");
}
```

---
#### Descartes

Mesmo que eu retorne essas informações, ex: "`Sucesso, linhasArquivo, QuantidadeLinhas`", eu não sou obrigado a usa-las. Por exemplo, podemos descartar: "`QuantidadeLinhas`".

```C#
LeituraArquivo Leitura = new LeituraArquivo();

var (sucesso, linhasArquivo, quantidadeLinhas) = Leitura.LerArquivo("Arquivos/arquivo.txt");

if (sucesso)
{
    Console.WriteLine("Quantidade linhas do arquivo: " + quantidadeLinhas);
    foreach(string linha in linhasArquivo)
    {
        Console.WriteLine(linha);
    }
}
else
{
    Console.WriteLine("Não foi possível ler o arquivo");
}
```

Então quando não estamos usando `quantidadeLinhas`, nesse caso. simplesmente colocamos um: `_`

```C#
LeituraArquivo Leitura = new LeituraArquivo();

// _ = Essa informação você descarta
// Serve pra deixar o código mais limpo
var (sucesso, linhasArquivo, _) = Leitura.LerArquivo("Arquivos/arquivo.txt");

if (sucesso)
{
    //Console.WriteLine("Quantidade linhas do arquivo: " + quantidadeLinhas);
    foreach(string linha in linhasArquivo)
    {
        Console.WriteLine(linha);
    }
}
else
{
    Console.WriteLine("Não foi possível ler o arquivo");
}
```

---
#### Desconstrutor
*Ou Deconstruct*

- É uma ação inversa ao construtor:
	- *Constructor = constrói*
	- *Deconstruct = descontrói*
		O Desconstrutor não destrói, mas separa a construção
	
- Classe `Pessoa` completa:
	```C#
	public class Pessoa
	    {
	        public Pessoa() 
	        {
	
	        }
	        public Pessoa(string nome, string sobrenome)
	        {
	            Nome = nome;
	            Sobrenome = sobrenome;
	        }
	
	        public void Deconstruct(out string nome, out string sobrenome)
	        {
	            nome = Nome;
	            sobrenome = Sobrenome;
	        }
	        private string _nome;
	        private int _idade;
	        public string Nome 
	        { 
	            get => _nome.ToUpper();
	            
	            set
	            {
	                if(value == "") 
	                { 
	                    throw new ArgumentException("O nome não pode ser vazio, espertão");
	                }
	
	                _nome = value;
	            } 
	        }
	
	        public string Sobrenome { get; set; }
	        public string NomeCompleto => $"{Nome} {Sobrenome}".ToUpper();
	
	        public int Idade 
	        {
	             get => _idade;
	             
	             set{
	                if(value < 0) {
	                    throw new ArgumentException("A idade não pode ser menor que zero.");
	                };
	
	                _idade = value;
	             }
	        }
	
	        public void Apresentar()
	        { 
	            Console.WriteLine($"Nome: {NomeCompleto}, Idade {Idade}");
	        }
	    }
	```
	
- Parte importante
	```C#
	public class Pessoa
	{
		public Pessoa() 
		{
		
		}
		public Pessoa(string nome, string sobrenome)
		{
			Nome = nome;
			Sobrenome = sobrenome;
		}
		
		// Ele aloca de forma contrária ao Constructor
		public void Deconstruct(out string nome, out string sobrenome)
		{
			nome = Nome;
			sobrenome = Sobrenome;
		}
		...
	}
	```
	
- Na prática
	```C#
	Pessoa p1 = new Pessoa("Leonardo", "buta");
	
	(string nome, string sobrenome) = p1;
	
	Console.WriteLine($"{nome} {sobrenome}");
	```
	
	```output
	LEONARDO buta
	```

Basicamente serve pra separar as propriedades construídas de uma classe, para operarem individualmente

### `IF` Ternário
*alternativa do `if()` onde podemos representar uma sintaxe diferente para representar `if else` e também apresentar uma melhor legibilidade ao código*

- Maneira tradicional
	```C#
	int numero = 15;
	
	if (numero % 2 == 0)
	{
		Console.WriteLine($"O número {numero} é par");
	}
	else
	{
		Console.WriteLine($"O número {numero} é impar");
	}
	```
	É um código muito verboso, para uma tarefa tão simples

- `IF` Ternário
	```C#
	int numero = 15;
	bool ehPar = false;
	
	ehPar = numero % 2 == 0;
	
	Console.WriteLine($"O número {numero} é " + (ehPar ? "par" : "ímpar"));
	```
	Assim é mais simples