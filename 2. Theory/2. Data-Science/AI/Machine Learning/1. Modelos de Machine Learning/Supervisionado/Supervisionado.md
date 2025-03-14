No aprendizado supervisionado, a máquina aprende a partir de dados rotulados, ou seja, dados que já possuem a resposta correta associada a eles. É como ensinar uma criança mostrando exemplos e dizendo qual é a resposta certa para cada um.

Se você conhece os dados, dá para você ajudar a máquina no aprendizado supervisionado.

A máquina aprende a mapear as variáveis de entrada (independentes) para os resultados conhecidos (variável dependente ou saída). Em outras palavras, aprende a prever a saída com base nas entradas.

Nele você aproxima:
	*as variáveis*  <-------------->  *os resultados conhecidos.*

---
### Dados Rotulados ([[Dados Rotulados]])

Dados rotulados são a base do aprendizado supervisionado. Eles consistem em pares de entrada-saída, onde cada entrada possui uma saída correspondente.

> [!example] Exemplo de Dados Rotulados:
> 
> Para prever o tempo de chegada em casa, podemos criar um conjunto de dados rotulados com as seguintes entradas (variáveis independentes):
> 
> - Condições climáticas
>     
> - Horários
>     
> - Feriados
>     
> 
> E a saída (variável dependente):
> 
> - Tempo que levou para chegar em casa em cada dia.
>     

Usando técnicas como a [[Regressão]] estatística, podemos analisar como as variáveis independentes (entradas) afetam a variável dependente (saída).

> [!info] Intuitivamente, sabemos que a chuva aumenta o tempo de viagem. As máquinas, porém, precisam de dados para aprender essa relação. Elas analisam os tempos de trajeto e os comparam com os dados rotulados de condições climáticas.

---
### Criando um Modelo Supervisionado

1. **Conjunto de Treinamento ([[Conjunto de Treinamento]]):** Criamos um conjunto de dados rotulados para treinar a máquina. No exemplo da previsão do tempo de chegada, a máquina aprenderia que:
    
    - Mais chuva geralmente implica mais tempo de viagem.
    - Horários de pico (próximo às 17h) também aumentam o tempo de viagem.
    
2. **Conjunto de Teste:** Após o treinamento, usamos um conjunto de dados separado (conjunto de teste) para avaliar a performance do modelo. Isso garante que o modelo generalize bem para dados não vistos durante o treinamento.
    
3. **Feedback e Ajustes:** Quanto mais testes e feedback a máquina recebe, mais preciso o modelo se torna. Novos dados podem ser incorporados para ajustar e aprimorar o modelo ao longo do tempo.
    

---
### Diferença com outros tipos de Aprendizado de Máquina

A principal diferença entre o aprendizado supervisionado e outros tipos de aprendizado de máquina (como o [[Não supervisionado]] e o [[Semi-Supervisionado]]) é a utilização de dados rotulados. No aprendizado supervisionado, a máquina aprende a prever a saída correta com base em exemplos já conhecidos. Nos outros tipos, a máquina precisa descobrir padrões e estruturas nos dados sem a ajuda de rótulos.

---
#machine-learning 