#machine-learning

---
## Contexto:

Na série Silicon Valley, da HBO, um dos personagens usa o aprendizado de máquina para resolver um problema real. 

Ele fotografa a comida à sua frente com um smartphone. Então, o aplicativo informa se é um cachorro-quente. Ele batizou o aplicativo como Not Hotdog. Ele criou o aplicativo usando um pequeno conjunto de treinamento de fotos de cachorros-quentes e processando milhões de fotos de comida on-line. 

Basicamente, usou o aprendizado [[Supervisionado]] para fazer uma [[classificação binária]]. Embora muitos problemas usem o aprendizado supervisionado, geralmente eles se enquadram nas seguintes categorias.

---
# A primeira é a [[classificação binária]]
*como vimos no caso do Not Hotdog...*

Depois, vem a [[classificação multiclasse]] e, por último, os problemas de [[Regressão]]. Cada categoria normalmente usa o mesmo tipo de algoritmo de aprendizado de máquina. 

O Not Hotdog usou um método estatístico para verificar a probabilidade de a imagem conter um cachorro-quente. 

Isso é uma classificação binária, um dos desafios mais comuns no aprendizado de máquina. Com a classificação binária, existem apenas dois resultados possíveis. Geralmente sim ou não. 

O quarto de hotel será reservado na próxima semana? A bolsa de valores subirá esta tarde? Esta imagem contém um cachorro-quente? Há uma resposta predefinida sobre o que é certo ou errado. ==Toda classificação binária usa aprendizado supervisionado. ==
<!--SR:!2023-09-19,3,250-->

---
> [!info] Lembre-se: o aprendizado supervisionado depende de dados rotulados. 
> Ou seja, alguém ensina ao computador um pouco sobre o que é certo ou errado.

 É preciso que um desenvolvedor defina os critérios no início. Você mostra à máquina uma imagem com um cachorro-quente. 
 
---
*Outro problema comum no aprendizado de máquina é a...*
# [[classificação multiclasse]]


#### Nesse problema, as categorias possíveis são quase **ilimitadas**. 

Para isso, você pode imaginar um aplicativo que analise a imagem de um alimento e o classifique com base em categorias pré-definidas. Talvez algo como sanduíches, bebidas ou assados. 

Então, você usaria outro conjunto de algoritmos estatísticos para colocar os dados nessas categorias. 

*(Você verá alguns desses algoritmos nos próximos vídeos)*. 

---
*Outra área muito interessante de aprendizado de máquina trata os...*
# Problemas de [[Regressão]]. 

Diferentemente da classificação binária e multiclasse, esses problemas tendem a ter uma solução contínua. Aqui buscamos tendências em vez de tentar classificar os dados em grupos. 

Imagine se um quarto de hotel será ou não reservado. Aqui se trata de uma classificação binária, pois existem apenas dois resultados possíveis. Isso é útil, mas saber quantos quartos provavelmente serão reservados seria mais útil. 

Aqui não há resultados predefinidos. Não é uma pergunta com resposta sim ou não. Há uma gama de possibilidades mais ou menos prováveis. Você pode usar a estatística e prever que entre 40 e 50 quartos estarão disponíveis. 

==Como na classificação binária, as regressões usam o aprendizado supervisionado==. Reforçando, é preciso mostrar à máquina o que significa um quarto estar ocupado ou livre. Então será usada a regressão linear. Os diagramas mostrarão uma linha de tendência que ajuda a prever quantos quartos serão ocupados. 