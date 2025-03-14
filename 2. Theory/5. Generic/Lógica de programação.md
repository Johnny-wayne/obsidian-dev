---
tags:
  - Fundamentos
---

---- 
## Ciclo de Desenvolvimento de Software
--- 
- ##### Estágio 1 - idealização


--- 
- ##### Estágio 2 - Especificação de Requisitos


--- 
- ##### Estágio 3 - Validação de Requisitos


--- 
- ##### Estágio 4 - Desenvolvimento e Testes


--- 
- ##### Estágio 5 - Implementação e Entrega



---- 

## 

var  salário = 30
var  horas = 30


var salário_por_horas = salário/horas


--- 
## Método 5Q´s 

1. Quais são os dados de entrada necessários?
2. O que devo fazer com estes dados?
3. Quais são as restrições deste problema?
4. Qual é o resultado esperado?
5. Qual é a sequência de passos a ser feitas para chegar ao resultado esperado?

--- 
```python
If (telefone == true): {
	telefone.ligar(id = 11, numero= 960948443)
} else {
	telefone.mensagem = "Ae, pau no cú, atende"
}
```

---

```python
valor_aleatorio = valor_aletorio.random(1:10)

chute = input(int("chute um número"));
print(chute)

if(número_aleatório == chute): {
	print("Valor tá certo")
} else if(chute > valor_aleatorio): {
		print("O número é menor, faz de novo");
		print(chute)
	} else if(chute < valor_aleatorio): {
			print("O número é maior, faz de novo");
			print(chute)
		} 

```

---- 
## Criando pseudocódigos

Tipos
1. Pseudocódigo
2. Fluxograma


```python
input valor_um
input valor_dois

if valor_um > valor_dois = print valor_um é maior
else = print valor_dois é maior
```

---

***Fatorial de um número***
``` Python
input numero
# numero = 5

if numero < 0
 print "digite apenas números positivos"
 
fatorial = 1
i = 1 

loop de i <= numero 
 fatorial = fatorial * i
 i = i + 1
 
 # fatorial = 1 * 1 = 1 | i = 2
 # fatorial = 1 * 2 = 2 | i = 3
 # fatorial = 2 * 3 = 6 | i = 4
 # fatorial = 6 * 4 = 24 | i = 5
 # fatorial = 24 * 5 = 120 | i = 6
 
print ("O fatorial de" + numero + " é : " + fatorial)
```

> [!question] Some os valores de uma lista
> Dados uma coleção de dados "idades" `[15,46,75,34,23]`
> ```python
> idades = [15,46,75,34,23]
>
> total = 0
> loop idade em idades
>	total = total + idade
>
> print("O total das idades são de: " + total)
> ```

> [!question] Chute o número 
>
> Escreva um programa que, ao iniciar gera um valor
aleatório de 1 a 10 e permite que o usuário chute um
número até que o valor aleatório gerado no início do
programa seja chutado corretamente. O programa deve
informar caso o chute tenha sido acima, abaixo ou igual
ao valor aleatório gerado no início do programa.

> [!failure] Se ele erra o código acaba
> ```python
> valor_aleatorio = valor_aletorio.random(1:10)
>
> chute = input("chute um número");
> print(chute)
>
> if(número_aleatório == chute): {
>	print("Valor tá certo")
> } else if(chute > valor_aleatorio): {
>		print("O número é menor, faz de novo");
>		input(chute)
>	} else if(chute < valor_aleatorio): {
>			print("O número é maior, faz de novo");
>			input(chute)
>		} 
> ```

> [!success] Enquanto ele não acertar, ele vai tentando

```python
valor_aleatorio = 1 a 10
tentativa = false

while(tentativa = false):
	chute = input("chute um número: ")
	if(chute > valor_aleatorio):
		print("chute maior que número")
	else if(chute < valor_aleatorio):
		print("chute menor que o número")
		tentativa = true
	else
		print("ACERTOU!!!")
```

---

## Fluxogramas

![[Fluxogram.png]]


<h2 align="center"> Vantagens e Desvantagens de Fluxogramas </h2>

| Vantagens                                                                                                                                                    | Desvantagens                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| * Fluxogramas podem ser mais intuitivos de entender para algumas pessoas.                                                                                    | * Caso tenha um processo altamente complexo, tentar o quebrar em passos em um fluxograma pode levar muito mais tempo que o pseudocódigo.                                                                                                                                                |
| * Fluxogramas podem abrir caminho para que pessoas não técnicas entrem no processo de design da  solução.                                                    | * O nível de detalhe da informação que é colocada em cada campo pode ter que ser simplificada para deixar o fluxograma mais legível.                                                                                                                                                    |
| * Caso tenha um processo altamente complexo, tentar o quebrar em passos menores em um fluxograma pode deixar a lógica mais explícita e de fácil compreensão. | * Ao tentar representar a lógica de um programa maior, terá um fluxograma possivelmente gigantesco e que não é facilmente lido, a não ser que tenho múltiplos monitores ou imprima o fluxograma em tamanhos grandes o suficiente para serem lidos em uma mesa no trabalho, por exemplo. |                                                                                                                                                                                                                                                                                         |
