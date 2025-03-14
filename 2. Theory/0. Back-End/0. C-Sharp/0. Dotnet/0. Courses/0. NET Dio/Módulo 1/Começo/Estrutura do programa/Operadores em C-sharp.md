
#### Convertendo variáveis

**Cast/Casting** - conversão de um tipo de variável pra outro

---
##### `Convert`

- De uma string pra um inteiro
	```C#
	int a = Convert.ToInt32("5");
	```
	- O `Convert` tem vários métodos que convertem para vários outros tipos de variáveis

---
##### `Parse`

- Literalmente a mesma coisa
```C#
	int a = int.Parse("5");
```

- Todos tipo tem o método `Parse`, menos o `string`

- Obs: aqui dá erro
	```C#
	int a = int.Pase("5c")
	``` 

---

##### Diferenças
É principalmente o tratamento de valores nulos

- Exemplo:
	- `Convert`
		```C#
		int a = Convert.ToInt32(null);
		Console.WriteLine(a);
		```
		- Output: `0`
		
	- `Parse`
		```C#
		int a = int.Parse(null);
		```
		- Output: `Value cannot be null; (Parameter 'a')`

*Obs: O professor recomenda o `Convert`*

---
##### Convertendo pra `String`


==A boa prática==
```C#
	int inteiro = 5;
	string a = inteiro.ToString();
```

Não existe:
```C#
	int inteiro = 5;
	string a = string.Parse(); 
```

Redundante
```C#
	int inteiro = 5;
	string a = Convert.ToString("a");
```

- Explicação:
	Toda classe vai herdar de uma classe `Object`, e a classe `Object` seria a mãe de todas as classes.
	
	E essa classe vai ter o método `ToString()`, que aplica pra todas as outras por causa da herança.

---
##### Cast Implícito
Uma conversão de diferentes tipos que você não precisa converter porque já faz automaticamente pra você.

- Ex: 
	```C#
	int a = 5;
	double b = a;
	```
	Tentar converter nesse caso, é redundante, porque um `int` cabe em um `double`, mesma coisa com: `long` e outros que cabem.
	
- O problema começa quando é o contrário:
	```C#
	long a = 5;
	int b = a;
```
	
	- Neste caso, precisaríamos realizar manualmente:
		```C#
		long a = 5;
		int b = Convert.ToInt32(a);
		```
	- Mas se fizermos assim dá pau tb:
		```C#
		long a = long.MaxValue; //valor máximo que o long é capaz (que é enorme)
		int b = Convert.ToInt32(a);
		```


---
##### Convertendo de maneira segura

Aqui dá erro, e como a gente sabe, tudo abaixo da onde deu erro, para.
```C#
	string a = "15-";
	int b = Convert.ToInt32(a);
	
	Console.WriteLine(b);
	Console.WriteLine("Conversão realizada com sucesso!");
```

Pra contornar isso, a gente usa o `TryParse()`
```C#
string a = "15-";
	int b = Convert.ToInt32(a);
	int b = 0;
	
	int.TryParse(a, out b);
	
	Console.WriteLine(b);
	Console.WriteLine("Conversão realizada com sucesso!");
```
- Ele fala o seguinte:
	- Vou tentar converter o `a`
	- Se der erro:
		- A gente usa o `b`
			- Output: `0`
	- Se não:
		- Output: `15`

#### Operadores Condicionais

##### `if()` aninhado:

```C#
if(maior == 0) 
{
	Console.WriteLine("Venda Inválida");
} 
else if(maior)
{
	Console.WriteLine("É maior");
}
else
{
	Console.WriteLine("É menor");
}
```
*basicamente quando tem um `else if`*

---
##### `switch case`

- Usando `if()`
	```C#
	Console.WriteLine("Digite uma letra");
	string letra = Console.ReadLine();
	
	if( letra == "a" ||
		letra == "e" ||
		letra == "i" ||
		letra == "o" ||
		letra == "u" )
	{
		Console.WriteLine("Vogal"); 
	}
	else
	{
		Console.WriteLine("Não é uma Vogal");
	}
	```

- Usando o `switch case`
	```C#
	switch (letra)
	{
		case "a":
		case "e":
		case "i":
		case "o":
		case "u":
			Console.WriteLine("Vogal");
			break; // saí do switch 
			
		default: // é como se fosse o else do switch
			Console.WriteLine("Não é uma vogal");
			break;
	}
	```

