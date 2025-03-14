*No Q-learning, a máquina deve melhorar a qualidade do resultado. É isso o que a letra “Q” representa.* 

---
**No Q-learning, há ambientes definidos, ou estados. Também existem ações possíveis para responder a esses estados.** 

- Estados = ambientes definidos
- Ações =  respostas
- Qualidade = Q

--- 

Você pode ter um jogo como o **Space Invaders**, no qual atira nos alienígenas para vencer. O sistema de recompensa é mais complexo. 

Não é tão simples como fazer com que o oponente erre a bola. Nesse caso, a qualidade inicial seria zero. 

Q = 0 (Inicial)
Q = 1 (Com base em melhorias)
Q = 2 (Com base em melhorias adicionais)

Depois, a máquina aprenderia quais ações melhorariam as condições. Cada vez que uma ação melhorasse o estado, o Q aumentaria. 

==Ele aumentaria com base nos estados e ações.==

---

> [!info] Traduzido do Inglês
> O Q-learning é um algoritmo de aprendizado por reforço sem modelo para aprender o valor de uma ação em um estado específico. Não requer um modelo do ambiente e pode lidar com problemas com transições estocásticas e recompensas sem exigir adaptações. [Wikipedia (inglês)](https://en.wikipedia.org/wiki/Q-learning)

---
#machine-learning 