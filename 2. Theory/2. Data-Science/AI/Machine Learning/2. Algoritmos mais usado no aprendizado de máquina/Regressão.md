K-means e K-NN são algoritmos baseados em instâncias ("preguiçosos"), fornecendo resultados apenas no momento da consulta. Qualquer alteração nos dados exige uma nova execução completa, tornando-os inadequados para escalonamento com grandes conjuntos de dados.

Para analisar relações numéricas contínuas entre diferentes partes dos dados, a **análise de regressão** é mais apropriada. Ela examina a relação entre preditores (variáveis de entrada, independentes ou regressores) e resultados.

Em aprendizado de máquina, os algoritmos de regressão funcionam iterativamente:

1. **Previsão:** Com os dados de treinamento, uma previsão é feita.
    
2. **Ajustamento:** A precisão da previsão é avaliada, e o algoritmo ajusta-se para melhorar a próxima previsão.
    
3. **Repetição:** Os passos 1 e 2 são repetidos até que a precisão seja satisfatória.
    
4. **Teste:** O modelo treinado é testado com dados não utilizados no treinamento (dados de teste) para avaliar sua generalização.
    

Este processo é supervisionado: os dados de treinamento são rotulados com os resultados corretos, que servem como base para o aprendizado e posterior previsão em dados de teste.

A **regressão linear** é um exemplo comum: ela cria uma linha reta que representa a relação entre o preditor e o resultado.
![[Regressão linear.png]]

Assim, vemos todos os pontos de dados agrupados em torno da linha reta, permitindo uma previsão mais precisa do resultado.

Para exemplificar, imagine que você é o proprietário de uma sorveteria e possui dados de vendas dos últimos 20 dias, juntamente com os dados meteorológicos correspondentes. Com esses dados de treinamento, você pode criar um gráfico de dispersão (diagrama de dispersão) com os eixos X e Y, distribuindo os pontos de dados no gráfico. O eixo X poderia representar a temperatura e o eixo Y, o número de picolés vendidos

![[gráfico de vendas.png]]

O eixo Y representaria as vendas diárias, e o eixo X, a temperatura (de 15 a 45 graus, para incluir todos os dados). A linha de melhor ajuste (hiperplano ou linha de tendência) seria traçada, dividindo os dados de forma a representar a relação entre temperatura e vendas. Um diagrama de dispersão mostraria uma tendência clara: temperaturas mais altas resultam em maiores vendas de sorvete.

Algumas vendas podem se desviar significativamente da linha de tendência (outliers/valores discrepantes) devido a eventos externos (festivais, por exemplo). Muitos outliers dificultam a previsão. No entanto, com poucos outliers, a regressão linear pode ser aplicada para prever as vendas. Por exemplo, com uma previsão de 35 graus, a linha de tendência indicaria vendas em torno de US$ 3.000.

A regressão linear não se limita a sorveterias; quanto mais dados, mais precisa a linha de tendência. Existe um debate se a regressão linear é ou não aprendizado de máquina, pois a "máquina" não aprende no sentido tradicional; ela apenas cria um modelo estatístico baseado nos dados. É mais uma ferramenta de previsão do que de aprendizado. O sucesso da regressão linear depende de encontrar preditores apropriados e uma relação linear entre eles e o resultado.

---
#machine-learning 