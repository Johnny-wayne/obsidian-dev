Árvores de decisão são úteis em problemas de classificação binária em aprendizado de máquina supervisionado. Elas permitem definir preditores e associá-los a um resultado, sendo facilmente visualizadas em diagramas de árvore.

**Exemplo: Carlos vai à praia?**

Vamos criar uma árvore de decisão para prever se Carlos irá à praia, usando três preditores:

- **Céu:** Nublado, Chuvoso ou Ensolarado.
    
- **Fim de semana:** Sim ou Não.
    
- **Velocidade do vento:** Alta ou Baixa.
    

O resultado (Carlos vai à praia?) é binário: Sim ou Não. Dados de treinamento seriam coletados e organizados em uma tabela com colunas para cada preditor e uma coluna para o resultado.

Exemplo de duas linhas de dados:

| Céu        | Fim de semana | Velocidade do vento | Carlos vai à praia? |
| ---------- | ------------- | ------------------- | ------------------- |
| Ensolarado | Sim           | Baixa               | Sim                 |
| Chuvoso    | Não           | Alta                | Não                 |

Para criar a árvore de decisão, os dados são divididos com base nos preditores. **O preditor "Céu" é escolhido como nó raiz (o tronco da árvore).**

O próximo nível são os **nós de decisão**, mostrando as opções do nó raiz (Nublado, Chuvoso, Ensolarado). Em cada nó de decisão, o número de resultados "Sim" e "Não" (Carlos foi ou não à praia?) é registrado com base nos dados de treinamento.

![[arvore.png]]

Com os dados de treinamento, existem quatro cenários em que Carlos vai à praia e três em que não vai. Esses resultados permitem a criação de nós folha (os galhos finais da árvore). Observe que, quando o nó de decisão é "Chuvoso", não há nós folha adicionais, pois Carlos nunca vai à praia em dias chuvosos. A árvore não precisa ser expandida nesse ramo. Após a construção da árvore de decisão, existe um caminho claro para cada resultado possível ("Sim" ou "Não" - Carlos vai ou não à praia).

![[arvore2.png]]

Se a árvore de decisão for difícil de interpretar ou apresentar muitos caminhos, pode haver alta **entropia**. Isso significa que a árvore está complexa e não fornece uma resposta clara ("Sim" ou "Não") de forma eficiente.

Por exemplo, no nó de decisão "Velocidade do vento", a análise mostra três ocasiões em que Carlos foi à praia com vento forte e duas com vento fraco. Essa ambiguidade indica entropia. Para reduzir a entropia, podemos usar um preditor diferente para dividir os dados neste ramo, ou até mesmo remover o preditor "Velocidade do vento", pois sua influência na decisão de Carlos não é clara.

Uma das grandes vantagens das árvores de decisão é sua facilidade de interpretação, mesmo para pessoas sem conhecimento profundo de aprendizado de máquina. A estrutura visual da árvore torna as decisões tomadas pela máquina transparentes e compreensíveis.

---
#machine-learning 