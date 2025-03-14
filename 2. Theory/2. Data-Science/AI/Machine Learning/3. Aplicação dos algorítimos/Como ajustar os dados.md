
No aprendizado de máquina, um **conjunto de treinamento** (subconjunto dos dados) é usado para ajustar algoritmos e criar um modelo que será aplicado a um **conjunto de teste** (o restante dos dados). A criação de um modelo eficaz requer um equilíbrio entre simplicidade e complexidade:

- **Subajuste (underfitting):** Um modelo muito simples pode funcionar bem com o conjunto de treinamento, mas falha ao generalizar para dados novos (conjunto de teste). Ele não captura informações suficientes dos dados, apresentando alto viés e baixa variância. Exemplo: um modelo que apenas considera tamanho e localização da casa para prever o valor, ignorando outros fatores relevantes (qualidade, reformas, etc.).
    
- **Sobreajuste (overfitting):** Um modelo muito complexo pode se ajustar perfeitamente ao conjunto de treinamento, mas falha ao generalizar para novos dados. É muito sensível ao ruído (variabilidade aleatória nos dados), apresentando baixa variância e alto viés. Exemplo: um modelo que inclui inúmeros preditores (vista, eletrodomésticos, distância de parques, etc.), tornando-se difícil de interpretar e generalizar para outras casas.
    

**Exemplo: Precificação de imóveis (Zillow)**

Um modelo para prever o valor de casas pode usar preditores como metragem quadrada, localização, número de banheiros e quartos. Entretanto, a variabilidade nos preços (ruído) pode exigir preditores adicionais (qualidade da vista, eletrodomésticos, etc.), aumentando a complexidade do modelo e potencialmente causando sobreajuste. Por outro lado, um modelo muito simples (apenas considerando tamanho e localização) pode ser um subajuste.

O objetivo é encontrar o equilíbrio ideal, capturando o máximo de **sinal** (informações úteis para previsão) e minimizando o **ruído** (variabilidade aleatória).

--- 
#machine-learning 