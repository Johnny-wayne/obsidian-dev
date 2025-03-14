
### Array

O Array é uma estrutura de dados que armazena valores do mesmo tipo, com um tamanho fixo.

1. `int[] array = new int[4];` - define como array de tamanho 4
2. `int[] array = new int[] {42, 75, 74, 61};` - aqui você pode omitir que ele já assume quanto tem
3. `string[] nomes = {"Jan", "Fev"};` - E você pode passar direto

Índice: É a posição de um determinado valor de um array, sempre começando com zero.

| Valores:     | 42    | 75    | 74    | 61    |
| ------------ | ----- | ----- | ----- | ----- |
| **Posição:** | **0** | **1** | **2** | **3** |

1. `int elemento = array[0];`
2. `array[0] = 42;`

---
##### foreach()
*Método que percorre uma lista sem precisar criar laços de repetição*

```C#
int[] arrayInteiros = {72, 64, 50, 1};
```


Percorrendo com o `for()`
```C#
	for(int contador = 0; contador < arrayInteiros.Length; Contador++)
	{ 
		Console.WriteLine($"Posição Nº {contador} + {arrayInteiros[contador]}");
	}
```

Percorrendo com `foreach(`
```C#
	foreach(int valor in arrayInteiros)
	{
		Console.WriteLine(valor);
	}
```
*Dá o mesmo resultado*

- A principal diferença, é que é mais difícil acessar o índice do array dentro do `foreach()`, caso quisermos acessar ele, é necessário instanciar um contador externo.

Dessa forma
```C#
	int contador = 0;
	foreach(int valor in arrayInteiros)
	{
	    Console.WriteLine($"Posição Nº {contador} - {valor}");
	    contador++;
	}
```

---
#### Redimensionando Arrays

```C#
	//estamos dobrando o tamanho do Array
	Array.Resize(ref arrayInteiros, arrayInteiros.Length * 2);
```

- **`Resize(referência do Array na memória, novo tamanho dele)`**
	- Ou
		```C#
			void Array.Resize<T>(ref T[]? array, int newSize)
		```

> Um array nasce e morre com a capacidade que foi definida no seu nascimento. O que o `Array.Resize()` faz é criar uma cópia do array, com o dobro do tamanho e apagar o antigo.

---
##### Copiando um Array para outro

```C#
	int[] arrayInteiros = {72, 64, 50, 1};
	
	int[] arrayInteirosDobrado = new int[arrayInteiros.Length * 2];
	Array.Copy(arrayInteiros, arrayInteirosDobrado, arrayInteiros.Length);
```

- `[arrayInteiros.Length * 2]` = 8
-  `Array.Copy(arrayInteiros, arrayInteirosDobrado, arrayInteiros.Length)`
	- Copiando de `ArrayInteiros`
	- Para `arrayInteirosDobrado`
	- Todo o Array, toda a capacidade

---
### Lista
*Um array "melhorado"*

É bem mais fácil de trabalhar porque não precisa definir tamanho nem ficar redimensionando. Tem mais facilidades em adicionar, remover, fazer consultas, etc.

Instanciando uma lista
```C#
List<string> lista = new List<string>();
```

---
#### Trabalhando com listas

Adicionando
```C#
	List<string> lista = new List<string>();
	
	lista.Add("SP");
	lista.Add("SP");
	lista.Add("SP");
```

- Com `for()`
	```C#
		for(int contador = 0; contador < lista.Count; contador++)
		{
			Console.WriteLine($"Posição Nº {contador} - {lista[contador]}");
		}
		//.Count pra listas é o equivalente ao .Length dos arrays
	```

- Com `foreach()`
	```C#
		int contador = 0;
		foreach(string item in lista)
		{   
		    Console.WriteLine($"Posição Nº {contador} - {item}");
		    contador++;
		}
	```

**Métodos e propriedades para se lembrar**
	- `lista.Count`
	- `lista.Capacity`


