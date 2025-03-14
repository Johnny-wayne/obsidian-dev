
## Selecionando Algoritmos de Aprendizado de Máquina: Um Guia

Ao selecionar uma linha na transcrição, você será direcionado à seção equivalente no vídeo.

Como especialista em aprendizado de máquina, a escolha do algoritmo certo para um desafio específico é crucial. Em alguns casos, as opções são limitadas.

**Aprendizado Supervisionado:** Se seus dados estão rotulados (com entradas e saídas conhecidas), o aprendizado supervisionado é a abordagem mais provável. Um exemplo é criar um aplicativo de precificação de casas, usando dados rotulados como código postal, metragem quadrada e número de banheiros. A máquina utiliza essas etiquetas para aprender os padrões sem precisar descobri-los sozinha.

**Aprendizado Não Supervisionado:** Com dados não rotulados, emprega-se o aprendizado não supervisionado. A máquina identifica padrões e agrupamentos por conta própria. Ao alimentar a máquina com dados de residências, ela pode agrupá-las com base em critérios como proximidade de áreas de fácil acesso, por exemplo. A análise desses agrupamentos fornece insights relevantes. O k-means clustering é um algoritmo popular para lidar com grandes conjuntos de dados não rotulados.

---
**Aprendizado Supervisionado: Escolha de Algoritmos**

Com dados rotulados, algoritmos como regressão, k-vizinho mais próximo e árvores de decisão são opções viáveis. Experimente diferentes algoritmos e analise cuidadosamente os resultados. Lembre-se: isso demanda tempo e recursos computacionais significativos.

**Exemplo:** Usando árvores de decisão, Naive Bayes e k-vizinho mais próximo em dados de treinamento, compare a precisão de cada um para determinar o melhor desempenho.

---
**Modelagem por Agrupamento (Ensemble Learning):**

Esta técnica combina múltiplos algoritmos para melhorar a precisão. Três métodos principais são:

- **Bagging:** Cria múltiplas versões do mesmo algoritmo (ex: múltiplas árvores de decisão com diferentes estruturas). A média dos resultados pode ser usada para reduzir a variância.
    
- **Boosting:** Combina múltiplos algoritmos, onde cada um corrige os erros do anterior, aumentando a precisão final. Um exemplo é combinar k-means clustering com uma árvore de decisão. Este método também se encaixa no aprendizado semi-supervisionado.
    
- **Stacking:** Empilha algoritmos, onde a saída de um algoritmo alimenta a entrada do próximo. O Feature Weighted Linear Stacking, usado pela equipe vencedora do prêmio Netflix, é um exemplo disso. Stacking algoritmos como k-vizinho mais próximo e Naive Bayes pode resultar em pequenas melhorias individuais, mas cumulativamente podem ser significativas. Algumas equipes em competições de aprendizado de máquina usam mais de 30 algoritmos em stack.
    

**Conclusão:**

Considere cada algoritmo como uma ferramenta. Experimente diferentes ferramentas e combinações para alcançar a melhor precisão em seus projetos de aprendizado de máquina.

---
#machine-learning 