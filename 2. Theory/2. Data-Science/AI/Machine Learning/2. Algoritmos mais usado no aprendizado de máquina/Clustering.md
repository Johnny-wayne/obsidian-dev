
> [!info] **Clustering**
  também conhecido como **análise de agrupamento**, é uma técnica de aprendizado [[Não supervisionado]] em que um conjunto de dados é dividido em grupos ou clusters com base em suas similaridades. O objetivo é agrupar elementos semelhantes juntos e separar elementos diferentes em grupos distintos, mesmo que você não saiba antecipadamente quais rótulos ou categorias esses grupos devem ter.

![[Clustering.png]]

--- 
### principais pontos sobre clustering:

1. **Semelhança:** A base do clustering é a medida de semelhança ou dissimilaridade entre os pontos de dados. Quanto mais semelhantes os pontos, maior a probabilidade de pertencerem ao mesmo cluster.
    
2. **Algoritmos de Clustering:** Existem vários algoritmos de clustering, cada um com abordagens diferentes para formar os clusters. Alguns exemplos populares incluem o K-Means, Hierarchical Clustering, DBSCAN e o Mean Shift.
    
3. **K-Means:** É um dos algoritmos mais conhecidos. Ele agrupa os dados em k clusters, onde k é um valor definido pelo usuário. Ele atribui pontos ao cluster mais próximo do centroide (ponto médio) do cluster.
    
4. **Hierarchical Clustering:** Esse método cria uma hierarquia de clusters, começando com cada ponto como seu próprio cluster e, em seguida, gradualmente mesclando clusters próximos, formando uma árvore de clusters.
    
5. **DBSCAN (Density-Based Spatial Clustering of Applications with Noise):** Este algoritmo identifica clusters baseados na densidade de pontos em torno de um ponto central. Ele pode lidar com clusters de diferentes formas e tamanhos, além de identificar pontos de ruído.
    
6. **Aplicações:** Clustering tem uma ampla gama de aplicações, incluindo análise de mercado, segmentação de clientes, agrupamento de documentos, análise de genes, reconhecimento de padrões em imagens e muito mais.
    
7. **Avaliação de Clusters:** Avaliar a qualidade dos clusters pode ser subjetivo, mas métricas como Silhouette Score e Inertia (para K-Means) são usadas para medir o quão compactos e separados os clusters estão.
    
Lembre-se de que o sucesso do clustering depende em grande parte da natureza dos dados e da escolha do algoritmo apropriado para o problema em questão. É uma ferramenta valiosa para explorar padrões e estruturas nos dados quando você não tem informações de rótulos ou categorias pré-existentes.

---
#machine-learning 