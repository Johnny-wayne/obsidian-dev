**Instruções:**

- Leia cada pergunta/exercício com atenção.
    
- Responda da forma mais completa possível.
    
- Para os exercícios práticos, escreva o código em C# como se estivesse em um editor de código. Não se preocupe com detalhes de sintaxe perfeitos, foque na lógica e estrutura.
    
- Tempo estimado: 20-30 minutos (se precisar de mais tempo, não tem problema).
    
---

**Perguntas de Múltipla Escolha (Escolha a melhor resposta):**

1. Qual das seguintes estruturas de dados é mais eficiente para buscar um elemento, dado que você conhece a sua posição (índice)?
    
    - (a) Lista encadeada
        
    - (b) Array (vetor)
        
    - (c) Pilha (Stack)
        
    - (d) Fila (Queue)
        
2. Qual é a complexidade de tempo, no pior caso, de uma busca linear em um array não ordenado de tamanho n?
    
    - (a) O(1)
        
    - (b) O(log n)
        
    - (c) O(n)
        
    - (d) O(n log n)
        
3. Qual dos seguintes algoritmos de ordenação é conhecido por ter uma complexidade de tempo média de O(n log n)?
    
    - (a) Bubble Sort
        
    - (b) Insertion Sort
        
    - (c) Selection Sort
        
    - (d) Merge Sort
    
4. Qual é a principal diferença entre uma `List<T>` e um array` T[]` em C#?
    
	-  (a) `List<T>` é imutável, enquanto `T[]` é mutável.
		
	- (b) `List<T>` tem tamanho fixo, enquanto `T[]` pode crescer dinamicamente.
		
	- (c) `List<T>` pode crescer dinamicamente, enquanto `T[]` tem tamanho fixo.
		
	- (d) Não há diferença significativa, ambos podem ser usados da mesma forma.
        


**Perguntas Discursivas:**

1. Explique, com suas palavras, o que é um algoritmo de busca binária e em que situações ele é mais eficiente do que uma busca linear.
    
2. Descreva a diferença entre uma pilha (Stack) e uma fila (Queue). Dê um exemplo de uso prático para cada uma dessas estruturas de dados.
    

**Exercícios Práticos (Coding Challenges):**

1. **Encontrar o Maior e o Menor:**  
    Escreva uma função em C# que receba um array de inteiros como parâmetro e retorne uma tupla (ou um objeto com duas propriedades) contendo o maior e o menor valor do array.
    
    ```c#
	// Exemplo de uso:
	int[] numeros = { 5, 2, 9, 1, 5, 6 };
	(int maior, int menor) = EncontrarMaiorEMenor(numeros);
	Console.WriteLine($"Maior: {maior}, Menor: {menor}"); 
	// Saída esperada: Maior: 9, Menor: 1
	
	// Sua função aqui:
	public static (int, int) EncontrarMaiorEMenor(int[] arr)
	{
	    // Implemente sua lógica aqui
	}
	```
	
2. **Inverter uma String:**  
    Escreva uma função em C# que receba uma string como parâmetro e retorne a string invertida.
    
	```c#
	// Exemplo de uso:
	string texto = "Hello, World!";
	string invertido = InverterString(texto);
	Console.WriteLine(invertido); // Saída esperada: !dlroW ,olleH
	
	// Sua função aqui:
	public static string InverterString(string str)
	{
		 // Implemente sua lógica aqui
	}
	```
        

3. **Verificar se um número é primo:**  
    Escreva uma função em C# que receba um número inteiro como parâmetro e retorne true se o número for primo e false caso contrário. Um número primo é aquele que é divisível apenas por 1 e por ele mesmo.
    
	```c#
	// Exemplo de uso:
    bool primo1 = EhPrimo(7);  // true
    bool primo2 = EhPrimo(10); // false
	
	// Sua função:
    public static bool EhPrimo(int numero)
    {
        // Implemente a lógica aqui.
    }
	```
        

---

Quando terminar, me avise para que eu possa revisar suas respostas e passar para o próximo teste. Bom trabalho!