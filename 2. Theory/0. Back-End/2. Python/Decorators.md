
Ele basicamente, atribui uma nova funcionalidade pra função que vem em baixo dele
```python
from flask import Flask

app = Flask(__name__)

@app.route('/home')
def homepage():
	return 'Essa é minha HomePage'

@app.route('/home')
def contatos():
	return 'Esses são meus contatos'
```

No caso do flask, essa nova funcionalidade é qual link ele vai aparecer

==Normalmente você encontra eles em Frameworks==
Criar eles, é meio chato, mas depois vira algo bem útil

---
#### O que é?

- Ele nada mais é do que uma função, que recebe como parâmetro, outra função e complementa ela

```python
import requests

#criar um decorator calcular_tempo
def calcular_tempo(funcao): 
	def wrapper():
		print('Vou pegar a cotação')
		funcao();
	return wrapper

@calcular_tempo
def pegar_cotacao_dolar():
	link = f"https://economia.awesomeapi.com.br/last/USD-BRL"
	requisicao = requests.get(link)
	requisicao = requisicao.json()
	print(requisicao['USDBRL']['bid'])

pegar_coatacao_dolar()

```

*Output:*
```
vou pegar a cotação 
5.6058
Peguei a cotação do dólar
```


##### Passo a passo
---
1. criar um decorator `calcular_tempo`
```python
def calcular_tempo(funcao): 
```

- Aqui eu acho que é só pra definir o decorator e pegar a função como parâmetro

---
2. definir a função `wrapper` que vai executar o código do decorator
```python
def calcular_tempo(funcao): 
	def wrapper():
```

---
3. Colocar as instruções da função `wrapper` e chamar a função que pegamos como parâmetro
```python
def calcular_tempo(funcao): 
	def wrapper():
		print('Vou pegar a cotação')
		funcao();
```


---
4. Retornar a função `wrapper()` para que ela seja executada quando chamarmos o decorator
```python
def calcular_tempo(funcao): 
	def wrapper():
		print('Vou pegar a cotação')
		funcao();
	return wrapper
```

---