
Aula anterior: [[Usando a classe Pessoa]]


-  Quebra de linha
	
	Isso
	```C#
	Console.WriteLine($"Olá, meu nome é {Nome} e tenho {Idade}");
	```
	
	É o mesmo que isso
	```C#
	Console.WriteLine($"Olá, meu nome é " +
					  $"{Nome} e tenho {Idade}");
	```

- `\n` pra quebrar a linha no `Console.WriteLine`

---
- Espaço em branco:
	```C#
	pessoa1
	.Nome = "Buta"
	```
	
	```C#
	pessoa1
	
	
	.Nome = "Buta"
	```
	
	```C#
	pessoa1        .    Nome = "Buta"
	```