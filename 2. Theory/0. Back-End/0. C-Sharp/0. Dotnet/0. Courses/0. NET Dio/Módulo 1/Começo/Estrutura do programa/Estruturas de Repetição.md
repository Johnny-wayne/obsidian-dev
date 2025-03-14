
- **While**
	- Se vc colocar `break` no laço de repetição `while()` ele para
		```C#
		while(contador <= numero)
		{
		    Console.WriteLine($"{numero} x {contador} = {numero * contador}");
		    contador++;
			
		    if(contador == 5)
		    {
		        break;
		    }
		}
		```
	- Menu interativo
		```C#
		string opcao;
		
		while(true)
		{
		    Console.WriteLine("Digite sua opção:");
		    Console.WriteLine("1 - Cadastrar cliente");
		    Console.WriteLine("2 - Buscar cliente");
		    Console.WriteLine("3 - Apagar Cliente");
		    Console.WriteLine("4 - Encerrar");
			
		    opcao = Console.ReadLine();
			
		    switch(opcao)
		    {
		        case "1":
		            Console.WriteLine("\nCadastro de cliente\n");
		            break;
		        case "2":
		            Console.WriteLine("\nBusca de cliente\n");
		            break;
		        case "3":
		            Console.WriteLine("\nApagar cliente\n");
		            break;
		        case "4":
		            Console.WriteLine("\nEncerrar\n");
		            Environment.Exit(0); // <-- saí do programa e do laço
		            break;
					
		        default:
		            Console.WriteLine("\nNúmero invalido\n");
		            break;
		    }
			
		}
			
			```
- **Do While**
	```C#
	int soma = 0, numero = 0;
	
	do 
	{
	    Console.WriteLine("Digite um número (0 para parar)");
	    numero = Convert.ToInt32(Console.ReadLine());
		
	    soma += numero;
		
	} while(numero != 0);
	
	Console.WriteLine($"Total da soma dos numeros digitados é: {soma}");

	```

