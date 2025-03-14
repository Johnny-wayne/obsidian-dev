
Aula anterior: [[Convenção case]]

##### Abreviações não são recomendadas

- Não recomendado
	```C#
	  public string NomeRepLegal { get; set; }
	```
	
- Recomendado
	```C#
	  public string NomeRepresentanteLegal { get; set; }
	```
	
	- Ou até mesmo:
		```C#
		  public string NomeRepresentanteLegalPessoaFisica { get; set; }
		```

---
É de boa prática colocar tanto o nome do arquivo quanto o nome da classe que ele está, como o mesmo.

- Ex: 
	- `Pessoa.cs` dentro do arquivo -->  `public class Pessoa`

