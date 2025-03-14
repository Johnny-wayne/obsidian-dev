- Aula anterior: [[Classe]]


Se formos no `NetDio/Program.cs` e escrevermos:

`'NetDio/Program.cs'`
```C#
Pessoa p new Pessoa()
```
*Vai dar pau*

---

Mas aqui não vai

`'NetDio/Program.cs'`
```C#
using NetDio.Models;

Pessoa p = new Pessoa();
```
*Porque podemos ter a classe `Pessoa` para multiplos contextos dentro do nosso programa, por isso usamos o  `using NetDio.Models`*

- Podemos ter duas classes com o mesmo nome, desde que tenham ***namespaces*** diferentes

---
###### Duas formas de se fazer:

- Primeira forma
	```C#
	using NetDio.Models;
	
	Pessoa p = new Pessoa();
	```

- Segunda forma
	```C#
	NetDio.Models.Pessoa p = new NetDio.Models.Pessoa();
	```
	- Só que fica enorme né