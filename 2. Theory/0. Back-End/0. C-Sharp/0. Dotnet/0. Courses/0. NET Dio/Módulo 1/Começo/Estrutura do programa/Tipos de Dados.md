- Tabela com os tipos de dados
	![[Pasted image 20240820182530.png]]

- Os mais usados em C# são:
	- string
	- object
	- bool
	- decimal
	- double
	- int
	
---
- O tipo `DateTime`
	```C#
	DateTime dataAtual = DateTime.Now; // Horário atual deste computador
	DateTime dataAtual = DateTime.Now.addDays(); // Adiciona dias a data atual
	DateTime dataAtual = DateTime.Now.addSeconds(); // Adiciona segundos 
	DateTime dataAtual = DateTime.Now.addMinutes(); // Adiciona Minutos 
		```
	*Esse tipo é um struct, ele é um pouquinho diferente de uma classe.* 
	
	```C#
	 	DateTime dataAtual = DateTime.Now.addDays(5);
	 	Console.WriteLine(dataAtual.ToString("dd/MM//yyyy")) //formato dia/mês/ano sem horário
	 	Console.WriteLine(dataAtual.ToString("dd/MM//yyyy HH:mm")) //formato dia/mês/ano Hora e Minuto (Sem milisecundos)
	```

