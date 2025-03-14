
Algoritmos de aprendizado de máquina supervisionados classificam dados, enquanto os não supervisionados os agrupam. Agora, exploraremos algoritmos baseados em probabilidade condicional – como um elemento afeta a probabilidade de outro ocorrer. O algoritmo Bayesiano, baseado na Teoria de Bayes, é amplamente utilizado, com o **Naive Bayes** sendo um exemplo popular.

**Naive Bayes: A Abordagem "Ingênua"**

O Naive Bayes recebe esse nome por assumir que os preditores são **independentes** entre si. É usado para classificação binária ou multiclasse. Considere novamente o abrigo de animais: queremos classificar cães em três categorias: Terrier, Caça e Esportivos, usando três preditores: comprimento do pelo, altura e peso. Embora existam correlações (um cão alto tende a ser mais pesado), o Naive Bayes trata cada preditor **independentemente**.

**Classificando um Cão Desconhecido**

Para classificar um cão desconhecido, o algoritmo calcula a "probabilidade dos preditores de classe":

1. **Comprimento do pelo:** O algoritmo determina a probabilidade do cão pertencer a cada classe com base nesse comprimento. Exemplo: 40% Terrier, 10% Caça, 50% Esportivo.
    
2. **Altura:** Independentemente do comprimento do pelo, a probabilidade é recalculada. Exemplo: 20% Terrier, 10% Caça, 70% Esportivo.
    
3. **Peso:** Novamente, independente dos preditores anteriores. Exemplo: 10% Terrier, 5% Caça, 85% Esportivo.
    

**Função de Multiplicação Ponderada**

Para combinar essas probabilidades, utilizamos uma função de multiplicação ponderada. Primeiro, atribuímos pesos a cada preditor, refletindo sua importância preditiva (baseada na análise dos dados de treinamento). Exemplo: Peso 3 para comprimento do pelo, e peso 2 para altura e peso. A classificação final se baseia na multiplicação da probabilidade de cada preditor por seu peso respectivo. Esse processo permite uma classificação mais precisa do cão desconhecido. Em cenários reais, com milhões de cães e grandes conjuntos de dados, esta abordagem se torna crucial para uma classificação eficiente.

---
#machine-learning 