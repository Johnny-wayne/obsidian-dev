---
Paradigm:
  - OOP
---
---
### Characteristics
 - Alto nível  
 - Dinâmica 
 - Fortemente tipada  
 - [[POO]]  
 - Identação define blocos
---
### Uso
- Desenvolvimento web
- Ciência de dados
- Automação de tarefas
- [[Machine Learning|Aprendizado de Máquina]] e inteligência artificial
- Desenvolvimento de jogos
- Desenvolvimento de linguagem

O Python é fácil de aprender e pode ser executado em muitas plataformas diferentes. A sintaxe simples e legível de Python torna a criação de scripts e a automação de tarefas uma tarefa fácil e acessível para os desenvolvedores. 

Em 2019, o Python se tornou a segunda linguagem mais utilizada do mundo.

---

## Basics
### Como funciona?  
  
1. Desenvolve o ***script***
2. Chama o [[interpretador]] Python  
3. Python compila e exibe os resultados na tela
---
Sintaxe: `nome_da_variavel`

  --- 
### Operadores:
*(colocando apenas os que eu não sabia)*

#### Matemáticos  
	** Exponenciação
	% Módulo
#### Relacionais
	<== divisão
	and
	or
	not
	E etc

*If* é um comando condicional, assim como o *else*

--- 
### Laços de Repetição

- Estruturas de repetição
- Iteradores  ***(iterar = Repetir)***
- Repetem um trecho de código
	- Enquanto a condição avaliada for verdadeira
	- Durante uma pré-determinada condição

***Exemplos***

```Python
x = 1

while x < 10: 
	print (x)
```
Aqui temos um loop infinito

```Python
x = 1

while x < 10: 
	print (x)
	x += 1
```
Aqui não

--- 
### Laço de repetição ***for*** (para)

***Exemplo***

```Python
lista1 = [1,2,3,4,5]

for i in lista1: 
	print(i)
	
```
para cada elemento da lista 1, printe o elemento

E o resultado vai ser:

1
2
3
4
5

O mesmo pode ocorrer com strings ou booleanos

---
### Combinação do ***for*** e ***range***

A função ***range*** retorna listas/arrays

`for i in range(10): print(i)`
irá retornar uma lista de 0 à 9

`for i in range(10,20): print(i)`
Vai de 10 até 19

`for i in range(10,20,2): print(i)`
Vai te 2 em 2 elementos
Logo retorna do 0 até o 18

--- 
### Objetos

#### Em Python, tudo é Objeto!
*Convencionou-se dizer que em Python tudo é um objeto. De fato, Python é uma linguagem orientada a objetos. [[POO]]*

##### Objetos são instâncias de classes. Por exemplo, quando você cria uma variável com uma _string_, você está criando um objeto do tipo  _string_.

Objetos possuem **atributos** (características) e **métodos** (ações que podem ser aplicadas).

Observe como verificar atributos e métodos a um objeto:

- #### objeto.atributo
    
- #### objeto.método( )

--- 
### Strings
```Python
a = "Diego"

print(a[0]) #D 
print(a[3]) #g

print(a[0:3]) #D i e g
```


Em Python ***Strings*** são ***Objetos***. 
Pode-se aplicar métodos a ***strings***.

#### string = string.método()
---
### Funções
*Elas permitem a **[[Modularização]]** do código*

São blocos de código que só são executados quando chamados
Em Python são definidas pela palavra reservada *def*


- #### Definição

*def* NOME(PARÂMETROS):
	COMANDOS

- #### Chamada
	NOME(ARGUMENTOS)


***Exemplo***

```Python
def soma (x, y):
	print(x + y)

soma(1,2)
```

> [!warning] 
> Caso chame X ou Y, retornará um erro.
> Pois tanto X quanto Y só existem no escopo do parâmetro da função.

Caso queira chamar algum dos parâmetros da função. Aqui uma solução:
```Python
def soma (x, y):
	return x + y

s = soma(1,2)
	print(s)
```

> [!tip] 
> Deixe as funções abaixo das váriaveis

```Python
s = soma(1,2)
	print(s)

def soma (x, y):
	return x + y

```



--- 
### Manipulação de arquivos

#### Abrindo Arquivos

- Função ***open***
- variável = ***open***(nome, modo)


| Modos | Funções   |
|---------|------------|
| r |  Só leitura |
| w | escrita (caso o arquivo já exista, ele será apagado e um novo arquivo vazio será criado)
| a | leitura e escrita(adiciona o novo conteúdo ao fim do arquivo)
| r+ | leitura e escrita |
| w+ | escrita (o modo w+, assim como o w, também apaga o conteúdo anterior do arquivo) |
| a+ | leitura e escrita (abre o arquivo para atualização) |

#### Lendo arquivos

- ***read()***
	- Lê o arquivo inteiro
- ***readline()***
	- Lê uma linha
- ***readlines()***
	- Lê o arquivo e o armazena em uma lista

```Python
arquivo = open("arquivo.txt")

print(arquivo)
```

Retornará:
`<_io.TextIOWrapper name='arquivo.txt' mode='r' enconding='UTF-8'>``

***readline()***
```Python
arquivo = open("arquivo.txt")

linhas = arquivo.readlines() #vai ler todas as linhas do arquivo e jogar dentro de uma lista

print linhas # vai retornar as linhas do arquivo
```

Também dá pra usar o ***for***:
```Python
arquivo = open("arquivo.txt")

linhas = arquivo.readlines()

for linha in linhas
	print(linha) 
```
***.read()***
```Python
arquivo = open("arquivo.txt")

texto_completo = arquivo.read()

print(texto_completo) 
```

#### Criando arquivos

```Python
w = open("arquivo2.txt", "w")

w.write("Esse é o meu arquivo")
```

```Python
w = open("arquivo2.txt", "a") # Lê e adciona no final do arquivo

w.write("Esse é o meu arquivo\n")

w.close() 
```
`w.close()` serve para fechar o arquivo. O Python já fecha por você.
Mas, às vezes pode fechar na linha errada e dar problema;

----
### Listas / Arrays

```Python
minha_lista_1 = ["abacaxi" ,"melancia", "abacate"]
minha_lista_2 = [1,2,3,4,5]
minha_lista_3 = ["abacaxi", 2, 9.89, True]

print(minha_lista_1[2])
# melancia
```

***error***
```Python
print(minha_lista_1[5])
# indexError
```

***For() in arrays***
```Python
for item in minnha_lista_1:
	print(item)
	# abacaxi
	# melancia
	# abacate
```

***Lenght***
```Python
tamanho = len(minha_lista_1)
print(tamanho)
# 3
```

***Adicionando***
```Python
minha_lista_1.append("limão")
print(minha_lista_1)
#['abacaxi', 'melancia', 'abacate', 'limão']
```

***Verificando se tem na lista:***
```Python
if 3 in minha_lista_2:
	print("3 esta na lista")
# 3 esta na lista
```

***Removendo elementos:***
```Python
del minha_lista_1[2:]
print(minha_lista)
# ['abacaxi', 'melancia']

del minha_lista_1[:]
print(minha_lista)
# []
```

***Ordenando listas:***
```python
lista = [124, 345, 5, 72, 46,6,7,3,1,7,0]

lista.sort()
print(lista)
# [0, 1, 3, 5, 6, 7, 7, 46, 72, 124, 345]
```
O método ***`.sort()`*** não retorna um valor, mas altera a própria lista, pois é ***`object.method()`***

Para retornar um valor seria necessário o método ***`Sorted()`*** e passar a lista como parâmetro
```principal
```

1. [[Métodos]] `array.sort()`**: O método `sort()` é um [[in-place]], o que significa que ele altera a própria lista original e não retorna uma nova lista ordenada. Ele reorganiza os elementos na mesma lista, mantendo a ordem dos elementos, mas modificando a estrutura original. Isso economiza memória, pois não cria uma nova lista.
    
```python
array = [3, 1, 2] 
array.sort() 
print(array)  # Saída: [1, 2, 3]
```
` .sort(reverse= True) `-   inverte para decrescente
Dá pra reverter a lista também:
`.reverse()```
    
2. [[Função]] `sorted(array)`**: A função `sorted()` retorna uma nova lista ordenada contendo todos os elementos da lista original. Ela não modifica a lista original e, em vez disso, cria uma nova lista ordenada a partir dos elementos da lista original. Isso é útil quando você deseja manter a lista original intacta.
    
```python
array = [3, 1, 2] 
sorted_array = sorted(array) 
print(sorted_array)  # Saída: [1, 2, 3] print(array)         
print(array) # Saída: [3, 1, 2]
```

Em resumo:

- Use `array.sort()` quando você desejar modificar a lista original e economizar memória ao fazer isso.
- Use `sorted(array)` quando quiser criar uma nova lista ordenada e manter a lista original inalterada.


---- 
### Dicionários

> [!info] Em Python, dicionários são arrays associativos, ou seja, um determinado valor passa a ser vinculado a uma chave. Exemplo:

```Python
# dicionarios em python
dicionario_sites = {"Diego": "diegomariano.com"}
```
  
No dicionário acima, a chave ***"Diego"*** foi vinculado ao valor ***"diegomariano.com"***. Assim, para imprimir o valor chame:

```Python
print(dicionario_sites['Diego'])
# Sera impresso "diegomariano.com
```
  

Se o dicionário tiver vários elementos, você pode usar laços para imprimi-los:

```python
 # dicionarios em python
dicionario_sites = {"Diego": "diegomariano.com", "Google": "google.com", "Udemy": "udemy.com"}

for chave in dicionario_sites:
     print(dicionario_sites[chave])
```

> [!Note] Dicionários são listas de associações compostas por: 
> - Uma chave
> - Um valor correspondente

```python
meu_dicionario = {"A":"AMEIXA", "B":"BOLA", "C","CACHORRO"}

print(meu_dicionario["A"])
# AMEIXA
print(meu_dicionario["B"])
# BOLA
print(meu_dicionario["C"])
# CACHORRO

for chave in meu_dicionario:
	print(meu_dicionario[chave])
#AMEIXA
#BOLA
#CACHORRO

for chave in meu_dicionario:
	 print(chave + ": " + meu_dicionario[chave])
# A: AMEIXA
# B: BOLA
# c: CACHORRO

```

##### Com funções:
```python
for i in meu_dicionario.items(): 
	print(i)
# ('A', 'AMEIXA')
# ('B', 'BOLA')
# ('C', 'CACHORRO')
```
Converte o dicionário em uma ***tupla/tuple***

> [!tip] Uma tupla ( tuple ) em Python
> **é uma sequência imutável de valores de qualquer tipo**. Para criar uma tupla, lista-se uma sequência de valores separados por vírgulas e, opcionalmente, entre parênteses. Tuplas são úteis para representar registros (mas sem atribuir nomes aos campos).

```PYTHON
for i in meu_dicionario.values(): 
	print(i)
#AMEIXA
#BOLA
#CACHORRO

for i in meu_dicionario.keys(): 
	print(i)
#A
#B
#C
```

---
### Tratamento de exceções

```python
a = 2
b = 0

print(a/b)

#Error
```
> [!error] este código daria erro, porque não dá pra dividir por 0


Por sorte, o **Python** tem um recurso de tratamento de exceções:
```python
a = 2
b = 0

try:
	print(a/b)
except:
	print("Não é permitida divisão por 0")

print(a/a)

#Não é permitida divisão por 0
#1.0
```
Ele mostra a mensagem e depois continua o código

---
### [[Exercícios]]

---
### Tópicos avançados em Python:

--- 
#### 1. **list comprehension**

Esse é o jeito simples:
```python
x = [1,2,3,4,5]
y = []

for i in x:
	y.append(i**2)

print(x)
#1,2,3,4,5
print(y)
#1,4,9,16,25
```

Esse é o ***List comprehension***
```python
y = [i**2 for i in x ]
#1,4,9,16,25
```
sintaxe: `y = [valor_a_adcionar laço condição]``

Outro exemplo pegando os ***números ímpares***
```python
z = [i for i in x if i%2==1]
print(z)
# 1, 3, 5
```
> [!note] Aqui é mais complexo, vamo lá:
> - `if i%2==1` se o resto da divisão de ***i*** por 2 for igual à 1 *(lembrando que em toda divisão impar, sobra 1)**

--- 
#### 2. **enumerate**

Navegar pela lista e pegar o index enquanto imprime

Jeito ***Não-pythonico***
```python
list = ["abacate", "bola", "cachorro"]

for i in range(len(list)): 
	print(i, list[i])
#0 abacate
#1 bola
#2 cachorro
```

Jeito ***Pythonico***
```python
for i, nome in enumerate(lista):
	print(i, nome)
#0 abacate
#1 bola
#2 cachorro
```
--- 
#### 3. **map**
*pegar função e aplicar a todos os elementos da lista*

```python
def dobro(x)
	return x*2

valor = 2
print(dobro(valor))
# 4
```

Mas....
```python
def dobro(x)
	return x*2

valor = [1,2,3,4,5]

print(dobro(valor))
# 1,2,3,4,5,1,2,3,4,5
```
aqui só vai repetir a lista, não aplicar o dobro

Usando o ***map()***:
```python
map(dobro, valor)
#map(função que quero chamar, lista que quero aplicar)
```
a função ***map()*** vai retornar um objeto do tipo '***map***', por isso precisamos atribui-lo a uma variável.

```python
def dobro(x)
	return x*2

valor = [1,2,3,4,5]

valor_dobrado = map(dobro, valor)

for v in valor_dobrado:
	print(v)
#2
#4
#6...

# pra adicionar em uma lista:
valor_dobrado = list(valor dobrado)
```
--- 
#### 4. **reduce**
*A função reduce() recebe uma lista e retorna um único valor pra ela*

```python
from functools import reduce

def soma(x,y):
	return x+y
	
lista = [1,3,5,10,20]

soma = reduce(soma, lista)
print(soma)
#39
```
--- 
#### 5. **zip**
*Função que concatena as listas*

```python
lista1 = [1,2,3,4,5]
lista2 = ["abacate", "bola", "cachorro", "dinheiro", "elefante"]

for numero, nome in zip(lista1, lista2): 
	print(numero nome)
#1 abacate
#2 bola
#3 cachorro
#4 dinheiro
#5 elefante
```

```python
lista1 = [1,2,3,4,5]
lista2 = ["abacate", "bola", "cachorro", "dinheiro", "elefante"]
lista3 = ["R$2,00","R$5,00", "não tem preço", "não tem preço", "não tem preço"]

for numero, nome in zip(lista1, lista2): 
	print(numero, nome, valor)
#1 abacate R$2,00
#2 bola R$5,00
#3 cachorro não tem preço
#4 dinheiro não tem preço
#5 elefante não tem preço
```

--- 
#### 6. **filter**

---
#linguagens 