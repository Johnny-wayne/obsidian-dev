
#### Concatenação de Strings

Podemos formatas valores em diversas representações. Essa formatação de valores é conhecida por concatenação ou interpolação.

Quanto você transforma um dado em outro, ou transformando ele em si ou juntando e formando outro.

Exemplo:
```C#
public void ListarAlunos() 
{
	Console.WriteLine($"Alunos de curso de {Nome}");
	
	for (int cout = 0; count < Aluno.Count; count++)
	{
		string texto = "Nº " + count + " - " + Aluno[count].NomeCompleto;
		Console.WriteLine(texto);
	}
}
```

Interpolação
```C#
	for (int cout = 0; count < Aluno.Count; count++)
	{
		string texto = $"Nº {count} - {Aluno[count].NomeCompleto}";
		Console.WriteLine(texto);
	}
```

---
##### Formatando valores monetários

```C#
decimal valorMonetario = 1004.40M;

Console.WriteLine($"{valorMonetario:C}")
```

- `82.40M;` 
	- O `M` é necessário no tipo `decimal` para identificar que estamos falando de moeda, dinheiro.
- `Console.WriteLine($"{valorMonetario:C}")`
	- Quando usamos o `:` significa que estamos escolhendo a formatação que vai ser exibida aquela propriedade. Nesse caso é `C` de *currency*
	- Outros tipos de formatação incluem `HH:mm`, `dd/MM/yyyy`, etc

	- *Output:*
	```
	R$ 1.004,40
	```
	Vai sair como R$ porque ele vai pegar a configuração do sistema para fazer a formatação

---
###### Alterando a localização do sistema

```C#
using ExemploExplorando.Models;
using System.Globalization;

CultureInfo.DefaultThreadCurrentCulture = new CultureInfo("en-US");

decimal valorMonetario = 1004.40M;

Console.WriteLine($"{valorMonetario:C}")
```

- `using System.Globalization;`
	- Importa saporra
- `("en-US")` 
	- É aqui que basicamente importa

- *Output*
	```
	$1,004.40
	```

- *Obs:*
	- Tome cuidado, porque essa cultura vai ser implementada em todo o sistema. Então não é ideal, caso vários usuários do mundo, usem.

###### Alterando a localização da cultura

```C#
using ExemploExplorando.Models;
using System.Globalization;

CultureInfo.DefaultThreadCurrentCulture = new CultureInfo("en-US");

decimal valorMonetario = 1004.40M;

Console.WriteLine(valorMonetario.ToString("C", CultureInfo.CreateSpecificCulture("enUS")));
```

- Sla mano, descobre

###### Formatação personalizada

``` C#
using ExemploExplorando.Models;
using System.Globalization;

CultureInfo.DefaultThreadCurrentCulture = new CultureInfo("pt-BR");

decimal valorMonetario = 1004.40M;

Console.WriteLine(valorMonetario.ToString("C1"));
```


- `C1` 
	- Representa quantas casas decimais ele vai representar, messe caso, seria:
		- `R$ 1.004,4`
- `N2` - Seria  a mesma coisa
---

##### Representando porcentagem

```C#
	using ExemploExplorando.Models;
	using System.Globalization;
	
	CultureInfo.DefaultThreadCurrentCulture = new CultureInfo("pt-BR");
	
	decimal valorMonetario = 1004.40M;
	
	Console.WriteLine(valorMonetario.ToString("C1"));
	
	double porcentagem = .3421;
	
	Console.WriteLine(porcentagem.ToString("P"));
```

- `ToString("P")`
	- Aqui basicamente define o formato
	- Esses tipos são formatações padrões no geral

- *Output*
	```
	34,21%
	```


- **Outros exemplos de formatação** 
	
	```C#
	int numero = 123456;
	Console.WriteLine(numero.ToString("##-##-##"));
	```
	
	- *Output*
		```
		12-34-56
		```

---
#### Formatando o tipo `DateTime`

*O tipo `DateTime` é na verdade uma `struct` uma estrutura no C#*

- Pré-code
	```C#
	using ExemploExplorando.Models;
	
	DateTime data = DateTime.Now;
	Console.WriteLine(data);
	```
	
	- *Output*
		```
		17/04/2022 18:25:59
		```

```C#
	DateTime data = DateTime.Now;
	Console.WriteLine(data.ToString("dd/MM/yyyy HH:mm"));
```

##### Formatando data e hora

- Data
	```C#
		DateTime data = DateTime.Now;
		Console.WriteLine(data.ToShortDataString());
	```
	
	- *Output -  `17/04/2022`* 

- Hora
	```C#
		DateTime data = DateTime.Now;
		Console.WriteLine(data.ToShortTimeString());
	```
	
	- *Output - `18:37`*

- Usando `Parse`
	```C#
		DateTime data = DateTime.Parse("17/04/2022 18:00"); // Podemos fazer assim tb, passando uma string que represente o valor do DateTime
		Console.WriteLine(data);
	```
	
	- *Output- `17/04/2022 18:00`*

##### Usando o `TryParse`

*Às vezes dá erro, porque nem sempre o formato ou o valor passado para o `DateTime` vai ser o correto, então precisamos usar o `TryParse` pra tratar dessas exceções*


```C#
	string dataString = "2022-13-17 18:00";
	
	DateTime.TryParseExact(dataString, 
						    "yyyy-MM-dd HH:mm", 
							CultureInfo.InvariantCulture, 
							DateTimeStryle.None, out DateTime data);
		
	Console.WriteLine(data);
```

- `dataString, "yyyy-MM-dd HH:mm"`
	- Essa data -> `dataString` tem esse formato -> `"yyyy-MM-dd HH:mm"` 
- `CultureInfo.InvariantCulture, DateTimeStryle.None` 
	- Servem mais pra falar que são independentes de estilo de data e localização, porque já passamos o formato que queremos
- `out DateTime data` 
	- Se ele conseguir converter ou não, ele vai jogar em na variável `data`

Aqui vai dar erro, porque tem o mês 13, vai retornar `01/01/0001 00:00:00`

Se arrumar, ele retorna certo.

##### Validando o retorno  do `TryParse
`
*`TryParseExact` retorna um booleano*

```C#
	```C#
	string dataString = "2022-13-17 18:00";
	
	bool sucesso = DateTime.TryParseExact(dataString, 
						    "yyyy-MM-dd HH:mm", 
							CultureInfo.InvariantCulture, 
							DateTimeStryle.None, out DateTime data);
	
	if(sucesso) 
	{
		Console.WriteLine("Conversão com sucesso! Data: {data}");
	} else
	{
		Console.WriteLine($"{dataString} não é uma data válida");
	}
	
	Console.WriteLine(data);
```

Retorna `true`

