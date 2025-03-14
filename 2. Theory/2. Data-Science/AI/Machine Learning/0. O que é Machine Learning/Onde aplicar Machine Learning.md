Quando um site ou app, apresenta uma seção de "Recomendado para você", provavelmente faz uso de Machine Learning. Ele é muito usado para coletar dados dos usuários para transformar a experiência em algo mais personalizado. Amazon analisa compra anteriores. Netflix analisa filmes assistidos anteriores. Youtube usa machine learning para traduzir automaticamente vídeos e etc.

> [!quote] No aprendizado de máquina, usa-se a inteligência artificial para ajudar o programa a encontrar padrões em conjuntos de dados massivos

### Pense em como uma máquina aprende:

Assim você consegue coletar dados de maior qualidade, suficientes e etc. Assim a máquina vê o mundo, não restrinja o programa

---

> [!note] Na programação tradicional de instruções explicitas: 
É colocada uma entrada (input) e assim é produzida uma saída (output) 
Sendo a entrada um comando e a saída uma resposta pré-definida.

---

#### Imagine que você esteja criando um programa para detectar mensagens de **Spam**, você pode criar um filtro para detectar anúncios ou vírus.

No Machine Learning, em vez de você colocar instruções, você insere dados, em vez de respostas pré-definidas vc trabalha com algoritmos de machine learning, para que ela aprenda responder.

**Para começar os dados são divididos em:**

- [[Dados de teste]]
- [[Dados de treinamento]]

>[!info] Dados de treinamento são usados para encontrar padrões, um modelo pode ajudar a entender os dados com algoritmos estatíscos. Esses algoritmos ajudam a máquina a fazer previsões precisas ou encontrar padrões.

--- 
## Exemplo em programa de Spam.

Temos 10 mil mensagens de e-mail como dados de treinamento que serão usados para criar e refinar o modelo antes de testar em 1 milhão de mensagens. Serve pra mostrar exemplos de spam.
Após isso você pode usar um algoritmo para classificar os e-mails em:

- Spams
- Mensagens comuns

>[!info] Isso é chamado de [[classificação binária]]
> A máquina faz isso descobrindo grupos de palavras mais prováveis de serem encontradas em mensagens de spam, em seguida atribui uma pontuação para mostrar a probabilidade de ser spam.

--- 

>Como especialista em aprendizado de máquina, você escolherá o melhor algoritmo de classificação a ser usado. Então você ajustará os hiper parâmetros do algoritmo até que a máquina se saia bem encontrando spams.
>Quando estiver satisfeito esse será seu modelo de dados inicial. Depois você coloca um algoritmo de aprendizado de máquina e ajusta os hiper parâmetros para que a classificação seja precisa. Por que no final, mesmo você colocando dados, algoritmos e parâmetros, quem decide se é spam ou não, é a máquina.


---
#machine-learning 