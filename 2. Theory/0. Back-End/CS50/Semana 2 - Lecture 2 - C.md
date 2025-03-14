Hello World - - > `$ code hello.c` - - > open or create new file called "hello"
```c
#include <stdio.h>

int main(void)
{
    printf("hello, world!\n");
}
```

prompt:
- `$ code hello.c` - create
- `$ make hello` - compile
- `$ ./hello` - run

Em C, boa parte das funcionalidades da linguagem, vem em arquivos separados, como o:
`<stdio.h>`
	Que faz com que `printf()` possa ser usado. Ou seja, `printf()` "vive" dentro do arquivo `<stdio.h>` que ensina o compilador, como printar coisas na tela.

---
`#include` 
	Basicamente diz pro compilador algo como:
		"Antes de tudo, procura no hard drive local, um arquivo chamado `stdio.h` e meio que *copy/past* ali, para que eu saiba sobre esse `printf()`"

---
O `.h` do `stdio.h` é basicamente chamado de *header file*, representa basicamente uma [[bibliotecas|biblioteca]] 

---
#### Functions

![[arguments - function - side effects]]

```c
void meow(void)
{ 
	printf("meow\n");
}
```

O primeiro `void`
	Diz que essa função não tem *valor de retorno*

O segundo `void`
	Diz que essa função não tem *argumentos*

> [!danger]
>  ```c
>  #include <cs50.h>
>  #include <stdio.h>
>  
>  int main (void) 
>  {
> 	 for (int i = 0; i < 3; i++)
> 	 {
> 		 meow();
> 	 }
>  }
> void meow(void)
> { 
>	printf("meow\n");
> }
> ```
assim vai dar pau


> [!warning]
>  ```c
>  #include <cs50.h>
>  #include <stdio.h>
>  
>   void meow(void)
> { 
>	printf("meow\n");
> }
> 
>  int main (void) 
>  {
> 	 for (int i = 0; i < 3; i++)
> 	 {
> 		 meow();
> 	 }
>  }
>
> ```
mas assim é zuado


> [!success]
>  ```c
>  #include <cs50.h>
>  #include <stdio.h>
>  
>  void meow(void);
>  
>  int main (void) 
>  {
> 	 for (int i = 0; i < 3; i++)
> 	 {
> 		 meow();
> 	 }
>  }
>  
> void meow(void)
> { 
>	printf("meow\n");
> }
>
> ```
então a gente faz assim

Dessa forma, o código tem uma "pista" de que por mais que a função não esteja definida ainda (antes do *main*), ele sabe que vai estar.


Mas, existe um jeito ainda melhor de se fazer isso:

```c
#include <cs50.h>
#include <stdio.h>

void meow(int n);

int main(void) 
{
	meow(30000);
}

void meow(void) {
	for(int = 0; i < n; i++)
	{
		printf("meow\n");
	}
}
```

---
##### `Calculator.c`

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int x = get_int("x: ");
    int y = get_int("y: ");
    
    printf("%i\n", x + y);

}
```

> [!error]
> ```c
> #include <cs50.h>
#include <stdio.h>
>
int main(void)
{
    int x = get_int("x: ");
    int y = get_int("y: ");
>
    printf(x + y);
}
>```

---
#### Scope

==error==
```c
#include <cs50.h>
#include <stdio.h>

int add(void);

int main(void)
{
	int x = get_int("x: ");
	int y = get_int("y: ");
	
	int z = add();
	printf("%i\n", z);
}
 
int add(void)
{ 
	return x + y;
}
```
Dá problema de escopo

Então a gente faz assim:
```c
#include <cs50.h>
#include <stdio.h>

int add(int a, int b);

int main(void)
{
	int x = get_int("x: ");
	int y = get_int("y: ");
	
	int z = add(x, y);
	printf("%i\n", z);
}
 
int add(int a, int b)
{ 
	return a + b;
}
```

---
Dá pra deixar ainda melhor se fizermos assim com `main`
```c
int main(void)
{
	int x = get_int("x: ");
	int y = get_int("y: ");
	
	printf("%i\n", add(x, y));
}
```
---

Ainda na função `main`, ela retorna `(void)`. Porque em todo programa que você escreve, quando ele termina de executar, ele retorna secretamente um número, se tudo ocorrer bem, ele *retornará 0* por convenção, se der ruim, ele retorna um inteiro. No caso da função `main`, é a mesma coisa.

---
#### [[Linux]]

Linux não tem lá muito [[Graphical User Interface - (GUI)]].

Neste curso, o codespace gerado como versão do vscode na nuvem, um software executado em um browser. Mas esse software, está conectado ao seu próprio servidor pessoal na nuvem, por assim dizer. 

Tecnicamente, é um "[[contêiner Docker]]", e esse servidor, ou contêiner está executando um sistema operacional chamado Linux. 

E toda vez que a gente usa o terminal do *codespace* do curso, ele manda da onde a gente tá escrevendo pra algum servidor na nuvem, no nosso próprio contêiner ou servidor Linux.

E pra usar melhor esse terminal, vc precisa aprender certos termos de terminal.

---
### Mario

```c
#include <stdio.h>

int main(void)
{
	//input para receber os dados de forma dinâmica
    const int n = get_int("Size: ");
	
	//repetição na vertical
    for (int index = 0; index < n; index++)
    {
	    //repetição horizontal
        for (int i = 0; i < n; i++)
        {
	        //impressão dos blocos
            printf("#");
        }
        //quebra de linha
        printf("\n");
    }
}
```

---

Se colocássemos `-1` como *input* de `n`, ele não retornaria nada. E isso é bom, mas se quiséssemos obrigar o usuário a colocar um numero inteiro positivo., teriamos que fazer assim:
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	
    int n = get_int("Size: ");
    while (n < 1)
    {
	    //porem aqui tem repetição:
        n = get_int("Size: ");
    }
    
    for (int index = 0; index < n; index++)
    {
        for (int i = 0; i < n; i++)
        {
            printf("#");
        }
        printf("\n");

    }

}
```

Pra resolvermos isso, nós usamos isso:

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	do
	{
		n = get_int("Size: ");
	}
	while (n < 1);
	
	for (int index = 0; index < n; index++)
	{
		for (int i = 0; i < n; i++)
		{
			printf("#");
		}
		printf("\n");
		
	}
	
}
```
Aqui a gente não declarou `n` direito, pq o certo seria `int n`
mas se fizéssemos isso dentro do *do while loop*, teríamos um problema de *escopo*.

Então fazemos assim:
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	int n;
	do
	{
		n = get_int("Size: ");
	}
	while (n < 1);
	
	for (int index = 0; index < n; index++)
	{
		for (int i = 0; i < n; i++)
		{
			printf("#");
		}
		printf("\n");
		
	}
	
}
```

---
##### Integer Overflow

Com três dígitos em decimal ou binário, nós conseguimos contar:

`001` -  1
`010` -  2
`011` -  3
`100` - 4  
`101` - 5
`110` - 6
`111` - 7

Mas pra contar até oito, precisariamos de um quarto digito:
`1000` - 8

Como não temos, o número volta a zero:
1`000`

É como se os zeros antes do um que falta para contar 8 fossem enganados, pensando que teriam espaço suficiente e obedecendo à ordem.

O nome desse erro é [[#Integer Overflow]]

Uma unidade de medida comum tem no mínimo 8 bits ou 1 byte, mas ainda mais comumente é 32. Com 32 bits é possível contar até:
- 4294967295
	- Só de número positivos

Se você estiver suportando números negativos também, vc vai precisar dividir esse número pela metade.
- 2147483647
&
- -2147483648

---
Em [[C]], você tem algum controle sobre quantos bits são usados.
- `int` por convenção são 32 bits
- `long` por convenção são 64 bits, não é o dobro, é exponencialmente maior.
	 Tem algumas coisas relacionadas à ele, como `get_long` e `%li`
		 `%li` vem de *long integer*

---
#### Truncation

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	int x = get_int("x: "); //1
	int y = get_int("y: "); //3
	
	printf("%i\n", x /  y);
	//Tudo certo né?
	//não..
}
```
Vai retornar 0, porque usamos `%i` que é para inteiros. Deveríamos usar `%f` para *floating numbers*.

Mas mesmo que fizéssemos:
```c
	printf("%f\n", x /  y);
```
Ainda daria erro.

Além dos números inteiros, nós temos:
- **float** - decimais (32bits)
- **double** - decimais (64bits) 

> O double significa que podemos usar mais números depois da casa decimal.

Então teoricamente, o certo seria fazer assim, certo? Lembrando que não precisamos declarar a variável `z`, mas para ficar mais didático:
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	int x = get_int("x: "); //1
	int y = get_int("y: "); //3
	
	float z = x / y;
	printf("%f\n", z);
}
```
Tudo certo né?

Não...
O resultado no prompt  é `0.000000`

Isso se deve a um problema que geralmente chamaremos, **Truncamento** ou **Truncation**. Basicamente é um termo bonitinho para dizer que como a operação matemática está sendo feita por inteiros, o resultado vai ser inteiro, mesmo que sobre `0.333333` ele vai simplesmente ser jogado fora ou *truncado*.

---
#### Type Casting

Para resolver isso, nós usamos **Type Casting**, que é converter um número inteiro em um float ou pelo menos trata-lo como tal, mesmo que não tenha um impacto matemático.
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	int x = get_int("x: "); //1
	int y = get_int("y: "); //3
	
	float z = (float) x / (float) y;
	printf("%f\n", z);
}
```

Agora sim, retorna: `0.333333`

Se vc dividir um `int` por um `int`, vc terá um `int`.

---
#### Float-Point Imprecision

Ainda com `z` sendo 1/3
Em `printf()`, você consegue definir o tanto de casas decimais que vc quer que apareçam.
```c
	printf("%f.5\n", z);
```
nesse caso, são 5 casas decimais.

E nesse caso será mostrado como resultado:
- `0.33333`

Mas nesse caso:
```c
	printf("%f.20\n", z);
```

O resultado será:
- `0.33333334326744079590`

Isso acontece porque o computador, tem uma *memória limitada*, e acaba dando esses erros, porque tenta arredondar pro mais próximo quando fica muito grande

No entanto...
Se usarmos `double`'s, em vez de `float`'s:
```c
double z = (double) x / (double) y;
printf("%.20f\n", z);
```

Vai dar algo como:
- `033333333333333331483`

Vamos ter mais números certos, mas ainda terá arredondamento.
Mais preciso, mas não é 100% preciso. Porque isso não será possível em termos de memória de computador.

---
Em 1999 para os anos 2000 deu ruim, porque virou o milênio. E teremos um problema parecido em 8 de janeiro de 2038.

