### Tipos
- [[Q-learning]]

--- 
> [!tip] Ele é diferente dos aprendizados [[Supervisionado]], [[Não supervisionado]] e [[Semi-Supervisionado]]

No aprendizado por reforço a máquina itera para melhorar continuamente o resultado. Com o tempo, a máquina deve se concentrar como um míssil teleguiado na busca de saídas de alta qualidade. O aprendizado por reforço é muito aberto.

--- 

Ele reforça o comportamento desejado para a máquina. ==Em vez de deixar tudo aberto para estudo e observação, você define um objetivo claro para a máquina. ==

Exemplo
Veja desta forma: quando eu era jovem, havia um jogo de videogame simples chamado Pong. O jogo tinha duas barras em lados opostos da tela, que deslizavam para cima e para baixo para tentarmos acertar a bola de cada lado. Em 2013, o projeto Deep Mind do Google fez um experimento com o Pong para ensinar um computador a jogá-lo.

Criaram várias recompensas para o computador. Toda vez que ele acertava a bola com a raquete, recebia uma recompensa. Toda vez que o adversário errava a bola, recebia outra recompensa. Depois, jogou contra si mesmo e tentou obter o máximo de recompensas. Em pouco tempo o computador dominou o jogo e começou a derrotar jogadores humanos. 

A equipe Deep Mind usou algo chamado [[Q-learning]]. O Q-learning ajudou em alguns dos jogos mais complicados que precisavam de recompensas mais sofisticadas. 

 O aprendizado por reforço é uma das áreas mais promissoras do aprendizado de máquina. A máquina passa por inúmeras simulações de ações e estados até encontrar a melhor estratégia. Em 2015, o projeto Deep Mind foi notícia quando seu programa AlphaGo venceu um jogador especialista no jogo chamado Go. O AlphaGo usou aprendizado não supervisionado. Aprendeu observando profissionais jogando Go. O novo programa AlphaGo Zero se baseia em Q-learning. Não precisa assistir aos especialistas jogando. O AlphaGo Zero analisou o jogo e tentou várias ações para mudar o estado e vencer. Em poucas horas, essa máquina de Q-learning jogou Go em um nível que os humanos não conseguem entender. Após apenas 70 horas de treinamento, o AlphaGo Zero venceu a versão anterior do AlphaGo nas primeiras 100 tentativas. O aprendizado por reforço e especificamente o Q-learning permitem que as máquinas avancem rapidamente além do nosso entendimento. Isso pode ajudar a pular as etapas requeridas pelo aprendizado não supervisionado. Não são necessárias horas observando e estudando grandes quantidades de dados.


---


# Aprendizado por Reforço

**Tipos:**

- [[Q-learning]]
    

> [!tip] Difere dos aprendizados [[Supervisionado]], [[Não supervisionado]], e [[Semi-Supervisionado]].

O aprendizado por reforço é um paradigma de aprendizado de máquina onde um agente aprende a tomar ações em um ambiente para maximizar uma recompensa cumulativa. A máquina itera continuamente, refinando suas ações ao longo do tempo, focando em resultados de alta qualidade. Seu funcionamento é baseado em um processo de tentativa e erro, guiado por um sistema de recompensas e penalidades.

## Conceitos Chave:

- **Agente:** A entidade que aprende e toma ações.
- **Ambiente:** O contexto onde o agente opera.
- **Estado:** A situação atual do ambiente.
- **Ação:** A escolha feita pelo agente.
- **Recompensa:** Um sinal numérico que indica o sucesso ou fracasso de uma ação.

## Diferenças de outros tipos de aprendizado:

Ao contrário do aprendizado supervisionado (que necessita de dados rotulados), ou não supervisionado (que busca padrões em dados não rotulados), o aprendizado por reforço define um objetivo claro e usa um sistema de recompensas para guiar o processo de aprendizado. É um processo mais exploratório e iterativo.

## Exemplo: Pong

Em 2013, o DeepMind (Google) utilizou aprendizado por reforço para ensinar um computador a jogar Pong. O computador recebia recompensas por acertar a bola e penalidades por errar. Através de inúmeras partidas contra si mesmo (aprendizado por reforço), ele aprendeu a maximizar suas recompensas, dominando o jogo e superando jogadores humanos.

## [[Q-learning]]:

Um algoritmo popular de aprendizado por reforço, o Q-learning, foi usado nesse experimento e em jogos mais complexos. Ele aprende a estimar o valor de realizar uma determinada ação em um dado estado, buscando a maximização da recompensa a longo prazo.

## Sucesso: AlphaGo e AlphaGo Zero

- **AlphaGo (2015):** Venceu um jogador profissional de Go usando aprendizado não supervisionado (aprendizado a partir da observação de jogos de profissionais).
    
- **AlphaGo Zero:** Uma versão posterior que utilizou Q-learning para aprender a jogar Go sem dados de jogos humanos, superando rapidamente a versão anterior.
    

## Vantagens do Aprendizado por Reforço:

- Permite que máquinas aprendam tarefas complexas sem a necessidade de grandes conjuntos de dados rotulados.
    
- Adaptação a ambientes dinâmicos e mudança de estratégias com o tempo.
    
- Potencial para superar o desempenho humano em algumas tarefas.
    

## Limitações:

- Pode ser computacionalmente caro e demorado, especialmente em problemas complexos.
    
- A definição de um sistema de recompensas eficaz é crucial para o sucesso do aprendizado.
    
- Pode ser difícil de lidar com ambientes estocásticos (com elementos aleatórios).
    

Este é um overview do aprendizado por reforço. Há muito mais detalhes e variações de algoritmos e técnicas a serem exploradas.
 
---
#machine-learning 