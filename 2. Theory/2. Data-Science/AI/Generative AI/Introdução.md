---
tags:
  - AI
  - machine-learning
aliases:
  - Introdução a machine-learning
---
--- 
# Definição:

A [[Generative AI]]  é um tipo de tecnologia de inteligência artificial que pode produzir vários tipo de conteúdo.
Incluindo:
- Texto,
- Imagens,
- Áudio,
- [[Dados sintéticos]]

---

*Tá mas o que é **IA (Inteligência Artificial)**?*
> [!Info] Inteligência Artificial 
> É a teoria e o desenvolvimento de sistemas computacionais que são capazes de performar tarefas normalmente precisam da inteligência humana.  Máquinas que pensam e se comportam como humanos.


*Qual sua diferença para o ML ou [[Machine Learning]]?*
![[Pasted image 20230809145200.png]]
[[Machine Learning]] dá ao computador a habilidade de aprender sem a programação explícita.

---
### Diferenças entre ML e Generative AI
- ***AI*** é a disciplina
- ***ML*** é um dos subtópicos dela
	- Dentro do ***ML*** existem outros subtópicos e outros dentro dele, como o [[Deep Learning]] que mexe com as redes neurais e suas implementações e configurações.
		-  Dentro do Deep Learning existem várias estruturas, uma delas é a [[Função de Ativação]], *(que pelo meu entendimento até agora é responsável pelo output das unidades de processamento)*.
			- Ele é um modelo de treinamento de máquina semi-supervisionado

- ###### A Generative AI é uma das subcategorias do [[Deep Learning]]. Isso significa que:
	- Usa redes neurais artificiais
	- Pode processar [[dados rotulados]] e não rotulados usando métodos: 
		- [[Supervisionado]]
		- [[Não supervisionado]]
		- [[Semi-supervisionado]]
Large Language Models (LLMs) também são uma subcategoria do [[Deep Learning]]

---
### Tipos de Modelos de Deep Learning

**IA Discriminativa ([[Discriminative AI]]):**

- Usado para classificar ou prever
- Tipicamente treinado a base de [[dados rotulados]]
- Learns the relationship between the features of the data points and the labels

**IA Indiscriminativa ([[Generative AI]]):**

- Gera novos dados que são similares aos dados com que foi treinada.
- Entende a distribuição de dados e o quão provável um exemplo dado é.
- Modelos de IA indiscriminativa podem ser usados para criar novos exemplos ou gerar novos dados realistas a partir do aprendizado da estrutura dos dados existentes.
- Exemplos incluem redes neurais generativas (GANs) e modelos de mistura de Gaussianas.

#### Exemplos

![[Discriminative & Generative.png]]

![[IA Models.png]]


> [!success] Is GenAI when `Y` is:
> - Natural Language
> - Image
> - Audio

> [!failure] Not GenAI when `Y` is a:
> - Number
> - Discrete
> - Class
> - Probability

$$
y = f(x)
$$
 $y  = Model Output$
 $f  = Model$
 $x = Input Data$

Se y é um numero como ***"Vendas previstas"*** não é GenAI
Se y é uma sentença como ***"Defina vendas"***

![[Model built.png]]

![[Gen IA Learning.png]]

#### Na programação tradicional
*Nós usamos regras para definir um animal*

***Programação tradicional***
```typescript
Cat:
	type: animal
	legs: 4
	ears: 2
	fur: yes
	likes: yarn, catnip
```

***Wave of Neural Networks | ~2012***
![[Wave of neural networks.png]]

***Generative language models | LaMDA, PaLM, GPT, etc.***
![[Generative Language Models.png]]

---
## O que é Generative AI?

- GenAI é o tipo de IA que cria novo conteúdo baseado naquilo que já aprendeu de conteúdo já existente.
- O processo de aprendizagem de conteúdo já existente é chamado de treinamento e resulta na criação de modelo estatístico
- Quando dado um prompt, GenAI usa esse modelo estatístico para prever o que pode ser uma resposta provável e isso gera um novo conteúdo.

|                                        Generative Language Models                                        |                                                                                   Generative Image models                                                                                   |
|:------------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Generative Language models aprendem sobre padrões na linguagem através de training data. Então dado um texto, ele prevê ***O que vem depois*** | Generative image models produzem novas imagens usando tecnicas como diffusion. Then, dado um promot ou imagem relacionadam eles ***transformam random noise em imagens ou geram imagens de prompts*** |

---
### Tipos de GenAI Baseadas em Dados:


<h2 align="center"> Image </h2>
![[Tyoe of Generative AI based on Image.png]]

<h2 align="center"> Text </h2>
![[Tyoe of Generative AI based on Text.png]]

> [!info]  GenAI
> Language Models aprendem sobre padrões na linguagem através de training data.
> Então, dado algum texto, eles preveem **O que vem a seguir** 


---
## Como funciona?

![[How it Works.png]]


```python

fatorial = input int(fatorial)

if(fatorial >= 0)

```


---

# Como funciona?



--- 
# Tipos de modelos:




---
# Aplicações que usam:


---