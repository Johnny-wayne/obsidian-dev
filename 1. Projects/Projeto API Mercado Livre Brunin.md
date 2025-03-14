
##### Definindo o ambiente virtual em python
```powershell
python -m venv envbrunin

```

Ativando o ambiente virtual
```powershell
envbrunin\Scripts\activate
```

Aí vai ficar assim, quando estiver no ambiente virtual
```powershell
sla sucesso
(envbrunin)

# OU

(envbrunin) $ C:\bla\blabla
```


### Código Inicial
```python
from flask import Flask, request
import requests

app = Flask(__name__)

@app.route('/notifications', methods=['POST'])
def handle_notifications():
    data = request.get_json()
    topic = data['topic']
  
    if topic == 'ORDERS':
        # Processar notificações de pedidos
        order_id = data['resource']['id']
        # ... fazer algo com o pedido ...
  
    return 'OK', 200
  
if __name__ == '__main__':
    app.run(debug=True)
```
*agente quer definir inicialmente um servidor local pra rodar a aplicação e usar a API do mercado livre na máquina e ir preenchendo certinho*

#### Entendendo o código inicial

##### **1. Importando Bibliotecas:**
 ```python
from flask import Flask, request
import requests
```

- **Flask:** Esta linha importa as classes e funções principais do framework Flask para criar uma aplicação web.
- **request:** Esta linha importa o objeto `request` do Flask, que fornece informações sobre a requisição **HTTP** recebida pela aplicação.
- **requests:** Esta linha importa a biblioteca `requests` para fazer requisições **HTTP** externas a partir da sua aplicação.

---
##### **2. Criando a Aplicação**

```python
app = Flask(__name__)
```

- Esta linha cria uma instância da classe `Flask` e a armazena na variável `app`. O argumento `__name__` é uma variável especial do Python que indica o nome do módulo atual.

---
##### **3. Definindo uma Rota:**

```python
@app.route('/notifications', methods=['POST'])
def handle_notifications():
    # ... código para processar notificações ...
    return 'OK', 200

```

- **Decorator `@app.route`:** Esta linha define uma rota para a sua aplicação. A rota é o caminho URL que acionará a função `handle_notifications`. No caso, a rota é `/notifications` e aceita somente requisições do tipo `POST`. Ou seja, essa função vai ser executada no `talvezlocalhost/notifications`
- **Função `handle_notifications`:** Esta função é executada sempre que a rota `/notifications` for acessada via [[HTTP POST]]

---
##### **4. Processando Notificações:**

```Python
data = request.get_json()
topic = data['topic']

if topic == 'ORDERS':
    # Processar notificações de pedidos
    order_id = data['resource']['id']
    # ... fazer algo com o pedido ...
```


- **`request.get_json()`:** Esta linha recupera o conteúdo da requisição HTTP no formato JSON e armazena-o na variável `data`.
- **`topic = data['topic']`:** Esta linha extrai o valor da chave `"topic"` do dicionário `data` e armazena-o na variável `topic`.
- **Condicional `if topic == 'ORDERS'`:** Esta condicional verifica se o valor da variável `topic` é igual a `"ORDERS"`. Se for verdadeiro, significa que a notificação é relacionada a pedidos.
    - **Extraindo ID do pedido:** Aqui, o código extrai o ID do pedido a partir do dicionário `data['resource']['id']` (supondo que a estrutura do JSON seja assim).
    - **Processamento:** A parte `# ... fazer algo com o pedido ...` representa o código que você precisa implementar para processar a notificação do pedido, como por exemplo, atualizar o banco de dados, enviar emails, etc.

---
##### **5. Retornando Resposta:**

```Python
return 'OK', 200
```

- Esta linha retorna uma resposta HTTP simples com o código de status 200 (OK) e a string "OK". Você pode modificar essa parte para retornar uma resposta JSON com mais informações dependendo da sua necessidade.

---
##### **6. Executando a Aplicação:**

```Python
if __name__ == '__main__':
    app.run(debug=True)
```

- Esta parte verifica se o script está sendo executado diretamente (não importado como módulo). Se for, executa o método `run` da instância `app` do Flask. O parâmetro `debug=True` habilita o modo debug, que é útil para desenvolvimento e fornece informações adicionais em caso de erros.