## Compiling

- `make`
	- Não compila para você, ele executa um outro comando por você, um compilador.
	- Não é um compilador, é um programa que automaticamente executa um compilador para você.

==hello.c==
```c
#include <stdio.h>

int main(void)
{
	printf("hello, world!\n";)
}
```
Para compilar este código por exemplo, digitaríamos `make` no prompt.

Mas o que na verdade acontece é que o `make` está executando um verdadeiro compilador para você. Chamado [[Clang]] para o [[C]].

Porém, [[Clang]] não é tão *user-friendly* assim.

Se você remover o arquivo que acabar de criar:
```
$ rm hello.c
```

E depois tentar compilar com o Clang:
```
$ clang hello.c
```
Ele irá permitir

Mas assim que formos tentar rodar o arquivo
```
$ ./hello
bash:./hello: no such file or directory
```

Isso acontece porque quando compilamos um código com o clang dessa forma, a *file* que ele cria para nós com o código compilado, é por *default*:
- `./a.out`
```
$ ./a.out
hello, world!
```

###### Command-Line Arguments
Palavras adicionais ou notações abreviadas, que você digitou no prompt de alguma forma e que modificou seu programa.

Se quiser criar um programa chamado `hello` e não `./a.out`, podemos fazer assim:
```
$ clang -o hello hello.c
```

Output:
```
$./hello
hello world!
```

Masssss...
Se tivermos com um código desse:
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	string name = get_string("What's your name? ");
	printf("hello, %s\n", name);

}
```

E tentarmos compilar desse jeito:
```
$ clang -o hello hello.c
```

vai dar ruim:
```
clang: error: linker command failed with exit code 1 (use -v to se invocation)
```

O que acontece, é que quando você vai usar um *third-party library*, ou só uma [[bibliotecas|biblioteca]]. Você precisa falar pro compilador que vc tá usando ela, mais ou menos desse jeito em Clang:

```
clang -o hello hello.c -lcs50
```

E aí você pode fazer o:
```
$ ./hello
What's your name? Johnny
hello, David
```

E é por causa desse trabalho todo que a gente usa o `make`.

---
### Source Code to Machine Code
*Compilar* é 1 dentre 4 processos que transformam código-fonte em 0 e 1.

Eles são:
- [[#Preprocessing]]
- [[#Compiling]]
- [[#Assembling]]
- [[#Linking]]

Quando você executa o [[Clang]], todas essas coisas acontecem.

---
##### Preprocessing

Toda linha que em [[C]], que começa com esse `#`, é o que chamam de *preprocessor directive*, não precisa ficar lembrando, mas tá aí.
```c
#include <cs50.h>
#include <stdio.h>
```

- Por exemplo
	Em ``#include <cs50.h>`` existe um protótipo da função, `get_string()`, com seus argumentos, valores de retorno e etc.

Então fazer isso
```c
#include <cs50.h>
#include <stdio.h>
```

É tão eficaz quanto fazer isso
```c
string get_string(string prompt);
int printf(string format, ...);
//Os três pontinhos mostram que é mais complicado do que parece
```

==De certa forma, isso é uma mentirinha, porque `printf()` deve ter seu próprio arquivo porque é uma biblioteca grande, mas a essência é essa==

---

#### Compiling

É basicamente transformar esse código-fonte:
```c
string get_string(string prompt);
int printf(string format, ...);

int main(void)
{
	string name = get_string("What's your name? ");
	printf("hello, %\n", name);
}
```

Nisso aqui: (Fiquei com preguiça de digitar tudo)

==assembly==
![[Pasted image 20240523171337.png]]

Mas se você prestar atenção, tem `get_string` e `printf` nesse código

---
#### Assembling

Ele basicamente pega o [[Assembly]] code, e transforma no que a gente se importa de vdd, que são os 0's e 1's, ou [[Machine Code]]

---
#### Linking

==hello.c==
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
	string name = get_string("What's your name? ");
	pfintf("Hello, %s\n", name);
}
```

Tecnicamente, em algum lugar do *Hard Drive/Disco Rígido* do computador, tem um arquivo chamado `cs50.c` e `stdio.c`, que realmente contém as implementações de `get_string()`, `get_int()`, `printf()`, mesmo que não esteja mencionado vc se refere a ele com `cs50.h` e `stdio.h`. 

Então neste pequeno código que está ali usa 3 arquivos

`hello.c` - `cs50.c` - `stdio.c`

O Clang precisa compilar, cada um deles, meio que separadamente, em 0's e 1's.

Mas aí a gente precisa juntar esses arquivos, e é aí que de uma forma inteligente, o compilador junta eles em um só pedação de 0's e 1's.

---
