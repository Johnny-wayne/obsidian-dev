
Os recursos de manipulação de exceção da linguagem C# ajudam você a lidar com quaisquer situações excepcionais ou inesperadas que ocorram quando um programa for executado.

### Realizando a leitura de um arquivo
*Criamos uma pasta `arquivos` e um `arquivo.txt` dentro, com 4 linhas de texto.*

Queremos fazer a leitura de um arquivo
```C#
using project2.Models;
using System.Globalization;



string[] linhas = File.ReadAllLines("Arquivos/arquivo.txt");

foreach(string linha in linhas) 
{
	// vai nos retornar 4 strings pq o arquivo tem 4 linhas
    Console.WriteLine(linha);
}
```

#### Disparando uma exceção

Nem sempre vem tudo bonitinho, no ambiente bonitinho, às vezes, dá merda. 

Por exemplo:
```C#
using project2.Models;
using System.Globalization;

//Alterando o caminho
string[] linhas = File.ReadAllLines("Arquivos/arqu_ivo.txt");

foreach(string linha in linhas) 
{
    Console.WriteLine(linha);
}
```

Se tu alterar o caminho, dá pau. Pq quando compilamos, ele não verifica se esse caminho existe. É aqui que retorna uma **<mark style="background: #FFF3A3A6;">Exceção</mark>***

Uma condição externa que o seu programa não tem como prever e reage parando o programa. Mas, ele para dando muitos detalhes, falando oq tentou fazer e dando pistas. Essa pista chama <mark style="background: #FFF3A3A6;">Stack Tracing</mark> - (rastro da stack).

#### Tratando uma exceção

Usando `try catch`
```C#
try 
{
    //vemos que esta linha pode ter uma exceção, e encapsulamos o código
    string[] linhas = File.ReadAllLines("Arquivos/arq_uivo.txt");

    foreach(string linha in linhas) 
    {
        Console.WriteLine(linha);
    }

} catch (Exception ex) 
{ 
    Console.WriteLine($"Ocorreu uma exceção genérica. {ex.Message}");
}
```

- `try catch`
	- Tenta realizar o código
	- Mas se der ruim, pega a exceção/erro e coloca na variável `ex` e executa o código dentro do `catch`

```Output
Ocorreu uma exceção genérica. Could not find file 'C:\Projetos\Videos\ExemploExplorando\Arquivos\arquivo.txt'.
```

Outra coisa interessante, é que quando alguma exceção ocorre dentro do `try` e o `catch` é executado, o resto do código fora do `try catch` também é executado, após o `catch`.

#### Exceção genérica e Exceção específica

Quando passamos o mouse por cima do método `ReadAllLines()` é possível ver algumas exceções específicas que retornam propriedades específicas do que ocorreu

- Exceções:
	![[Pasted image 20240901224810.png]]

Todas essas exceções herdam da classe mais genérica chamada `Exception`.

Podemos ter vários catch, e fazer um para cada Exceção.
```C#
try 
{
    string[] linhas = File.ReadAllLines("Arquivos/arq_uivo.txt");

    foreach(string linha in linhas) 
    {
        Console.WriteLine(linha);
    }
	
} 
catch (FileNotFoundException ex) 
{
    Console.WriteLine($"Ocorreu um erro na leitura do arquivo. Arquivo não encontrado. {ex.Message}");
}
catch (DirectoryNotFoundException ex)
{
    Console.WriteLine($"Ocorreu um erro na leitura do arquivo. Caminho da pasta não encontrado. {ex.Message}");
}
catch (Exception ex) 
{ 
    Console.WriteLine($"Ocorreu uma exceção genérica. {ex.Message}");
}
```

#### Bloco `finally`

```C#
	using project2.Models;
	using System.Globalization;
	
	try 
	{
	    string[] linhas = File.ReadAllLines("Arquivos/arq_uivo.txt");
	
	    foreach(string linha in linhas) 
	    {
	        Console.WriteLine(linha);
	    }
	
	} 
	catch (DirectoryNotFoundException ex) 
	{
	    Console.WriteLine($"Ocorreu um erro na leitura do arquivo. Caminho da pasta não encontrado. {ex.Message} ");
	}
	catch (FileNotFoundException ex) 
	{
	    Console.WriteLine($"Ocorreu um erro na leitura do arquivo. Arquivo não encontrado. {ex.Message} ");
	}
	catch (Exception ex) 
	{ 
	    Console.WriteLine($"Ocorreu uma exceção genérica. {ex.Message} ");
	}
	finally 
	{
	    Console.WriteLine("Chegou até aqui.");
	}
```

O bloco é executado, independente se der erro ou não.

#### `Throw`
*Quando jogamos uma exceção para ser pega para outro bloco de programa.*

Nova classe `Exce`
```C#
public class Exceção
{  
       public void Metodo1()
       {
            Metodo2();
       }
       public void Metodo2()
       {
            Metodo3();
       }
       public void Metodo3()
       {
            Metodo4();
       }
       public void Metodo4()
       {
            throw new Exception("Ocorreu uma exceção.");
       }
}
```

```output
	Unhandled exception. System.Exception: Ocorreu uma exceção.
	   at project2.Models.Exceção.Metodo4() in C:\Users\johnn\Desktop\project2\Models\Exceção.cs:line 24
	   at project2.Models.Exceção.Metodo3() in C:\Users\johnn\Desktop\project2\Models\Exceção.cs:line 20
	   at project2.Models.Exceção.Metodo2() in C:\Users\johnn\Desktop\project2\Models\Exceção.cs:line 16
	   at project2.Models.Exceção.Metodo1() in C:\Users\johnn\Desktop\project2\Models\Exceção.cs:line 12
	   at Program.<Main>$(String[] args) in C:\Users\johnn\Desktop\project2\Program.cs:line 6
```

###### `throw` 

- joga pra cima saporra aí, joga de volta, eu não sei oq tá acontecendo, logo eu tô jogando pra cima pra alguém tratar pra mim
	
- Quando fazemos o `throw` ele vai jogar pra alguém pegar, (pegar aonde karai), no `catch`, então ele vai jogando de baixo pra cima verificando se tem o `catch`
	- "Tem o `catch` método 3?" - Não
	- "Tem o `catch` método 2?" - Não
	- "Tem o `catch` método 1?" - Não
	- "Tem o `catch` `program.cs`?" - Não
	- ==Então encerra essa porra e dá erro aí==
	
- Por isso lemos de baixo pra cima
	
- Nesse caso estamos jogando uma *Exceção Genérica*

##### E si nois joga um `try catch`?

```C#
public class Exceção
{  
       public void Metodo1()
       {
            try 
			{
			   Metodo2();
			} 
			catch(Exception ex)
			{
				 Console.WriteLine("Exceção tratada" + ex.Message);
			}
       }
       public void Metodo2()
       {
            Metodo3();
       }
       public void Metodo3()
       {
            Metodo4();
       }
       public void Metodo4()
       {
            throw new Exception("Ocorreu uma exceção.");
       }
}
```

```output
	Exceção tratada. Ocorreu uma exceção.
```

Se não tiver ninguém que consiga tratar a exceção ele vai exibir o "`stack tracing`". Que é o rastro da *stack*, aonde ele tentou chegar.

- Se colocarmos:
	```C#
	try 
	{
	   Metodo2();
	} 
	catch(Exception ex)
	{
		 Console.WriteLine("Exceção tratada" + ex.StackTrace);
	}
	```

- Dá isso: 
	```stacktracing
	Exceçao tratada. at project2.Models.Exceção.Metodo4() in C:\Users\johnn\Desktop\project2\Models\Exceção.cs:line 24
		   at project2.Models.Exceção.Metodo3() in C:\Users\johnn\Desktop\project2\Models\Exceção.cs:line 20
		   at project2.Models.Exceção.Metodo2() in C:\Users\johnn\Desktop\project2\Models\Exceção.cs:line 16
		   at project2.Models.Exceção.Metodo1() in C:\Users\johnn\Desktop\project2\Models\Exceção.cs:line 12
	```

---

### Introdução a Filas - `Queue`
*Um tipo de coleção.*

- Já vimos os tipos de coleções:
	1. Array
	2. Lista
	Que nada mais são do que uma coleção de elementos do mesmo tipo que podem ser acessados por sua posição.

Temos Coleções que são diferenciadas por obedecerem e implementarem regras especificas, uma dessas estamos falando da `Queue` ou seja uma Fila.

- Como funciona uma fila? 
	- Funciona como uma fila normal, da vida real mesmo, as de supermercado.
- Quais são as regras?
	- A primeira pessoa da fila, vai ser a primeira a ser atendida
	- E a última pessoa que chegou vai pro último lugar da fila.
	- Uma coleção do tipo fila, obedece exatamente essas regras, não existe cortar fila aqui

- *Imagem de uma `Queue`*
	**![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUey85nyIfcK0hioCHEoXCzsYxgV9S9JabPQcVpTQ4FKgz3hoQt-SraNl15KCWpFZgh9Vg5T7QgJpYjzEFzNOxAcF1H1G_yMFXplEZ4fMdV73NtGBfmc3yEgWGxXTeMHRAY5KXr6SXMB_76-8ocS37oUwFIU3H0ce2ra4GQJMU1dGlpYOliQiB4=nw?key=wAdzpc9AwbMhy_eupWlVmw)**

>Essa regra de ***"Primeiro a Entrar, Primeiro a Sair"***
>Também é conhecida como ***FIFO - First In, First Out*** 

#### Fila na prática

```C#
Queue<int> fila = new Queue<int>();

//adiciona pro fim da fila
fila.Enqueue(2);
fila.Enqueue(4);
fila.Enqueue(6);
fila.Enqueue(8);

foreach(int item in fila)
{
    Console.WriteLine(item);
}

//sempre remove o primeiro elemento pq não dá pra remover o do meio
Console.WriteLine($"Removendo o elemento: {fila.Dequeue()}");
fila.Enqueue(10);

foreach(int item in fila)
{
    Console.WriteLine(item);
}
```

```output
	2
	4
	6
	8
	Removendo o elemento: 2
	4
	6
	8
	10
```
---
### Introdução a Pilhas - `Stack`
*Como a Coleção **Fila** elas obedecem algumas regras de inserção e remoção de seus elementos*

- Obedece a ordem: ***LIFO - Last In, First Out***

- Imagem de ***Pilha***
	![[Pasted image 20240902184859.jpg]]
	Brincadeira... rs 
	
	**![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUcLl5Od0cQN1gSjm6BD8U0WeiU-V7_FRnAf7WFmU8qoZtWSEJqZyRGPV9CMwmISVaJSWYWhSJmPqOxIWfvagjiWWqq_P9H0VMtrMkcO2lxBswdbKw0Ogg0my2g7zU82ImTkrWcHsIF6AxQX6wcHYSAxjPRcoTnPjlD98ZdM-f49njWA9BXJog=nw?key=wAdzpc9AwbMhy_eupWlVmw)**


#### Pilha na prática

- Imagem de Pilha na prática:
	![[Pasted image 20240902185148.jpg]]
	Brinca muito vsfd KAKKAKAKAKAAKKA

```C#
Stack<int> pilha = new Stack<int>();

//coloca no topo da pilha
pilha.Push(4);
pilha.Push(6);
pilha.Push(8);
pilha.Push(10);

foreach(int item in pilha)
{
    Console.WriteLine(item);
}

Console.WriteLine($"Removendo o elemento do topo: {pilha.Pop()}"); //10

pilha.Push(20);

foreach(int item in pilha)
{
    Console.WriteLine(item);
}
```

```output
	10
	8
	6
	4
	Removendo o elemento do topo: 10
	20
	8
	6
	4
```

- Ou seja, tiramos o 10 do topo da pilha e colocamos o 20 por cima

---
### Introdução `Dictionary`
*Um **Dictionary*** é uma coleção de chave-valor para armazenar valores únicos sem uma ordem específica.

```C#
Dictionary<string, string> estados = new Dictionary<string, string>();

estados.Add("SP", "São Paulo");
estados.Add("BA", "Bahia");
estados.Add("MG", "Minas Gerais");

foreach(KeyValuePair<string, string> item in estados)
{
    Console.WriteLine($"Chave: {item.Key}, Valor: {item.Value}");
}
```

- `KeyValuePair`
	- Tipo do `dictionary`, mas podemos substituir pela palavra `var` pq aí reconhece automaticamente.

```output
	Chave: SP, Valor: São Paulo
	Chave: BA, Valor: Bahia
	Chave: MG, Valor: Minas Gerais
```

- Cada chave (elemento que vem primeiro), dentro do `Dictionary` precisa ser único.
	```C#
	estados.Add("BA", "Bahia"); //aqui daria pau se adicionasse no código ali
	```
	
	```C#
	estados.Add("BA2", "Bahia"); //aqui daria o output aqui:
	```
	
	```output
	Chave: SP, Valor: São Paulo
	Chave: BA, Valor: Bahia
	Chave: MG, Valor: Minas Gerais
	```


#### Removendo e alterando elementos

- Removendo
	```C#
	Dictionary<string, string> estados = new Dictionary<string, string>();
	
	estados.Add("SP", "São Paulo");
	estados.Add("BA", "Bahia");
	estados.Add("MG", "Minas Gerais");
	
	foreach(KeyValuePair<string, string> item in estados)
	{
	    Console.WriteLine($"Chave: {item.Key}, Valor: {item.Value}");
	}
	
	estados.Remove("BA");
	
	foreach(var item in estados)
	{
		Console.WriteLine($"Chave: {item.key}, Valor: {item.Value}");
	}
	```
	Aqui vai tá sem a `BA`

- Alterando
	```C#
	Dictionary<string, string> estados = new Dictionary<string, string>();
	
	estados.Add("SP", "São Paulo");
	estados.Add("BA", "Bahia");
	estados.Add("MG", "Minas Gerais");
	
	foreach(KeyValuePair<string, string> item in estados)
	{
	    Console.WriteLine($"Chave: {item.Key}, Valor: {item.Value}");
	}
	
	Console.WriteLine("------------");
	
	estados.Remove("BA");
	
	//pegando o valor aqui e alterando
	estados["SP"] = "São Paulo - valor alterado";
	
	foreach(var item in estados)
	{
	    Console.WriteLine($"Chave: {item.Key}, Valor: {item.Value}");
	}
	```
	
	```output
	Chave: SP, Valor: São Paulo
	Chave: BA, Valor: Bahia
	Chave: MG, Valor: Minas Gerais
	------------
	Chave: SP, Valor: São Paulo - valor alterado
	Chave: MG, Valor: Minas Gerais
	```

- Verificando o elemento antes de adicionar:
	```C#
	Dictionary<string, string> estados = new Dictionary<string, string>();
	
	estados.Add("SP", "São Paulo");
	estados.Add("BA", "Bahia");
	estados.Add("MG", "Minas Gerais");
	
	string chave = "BA";
	Console.WriteLine($"Verificando o elemento: {chave}");
	
	if (estados.ContainsKey(chave))
	{
	    Console.WriteLine($"Já tem essa porra de {chave}");
	}
	else
	{
	    Console.WriteLine($"Valor não existe. É seguro adicionar a chave {chave}");
	}
	```
	
	```output
	Verificando o elemento: BA
	Já tem essa porra de BA
	```

- Acessando valores:
	```C#
	Dictionary<string, string> estados = new Dictionary<string, string>();
	
	estados.Add("SP", "São Paulo");
	estados.Add("BA", "Bahia");
	estados.Add("MG", "Minas Gerais");
	
	Console.WriteLine(estados["MG"]);
	```
	
	```C#
	Minas Gerais
	```