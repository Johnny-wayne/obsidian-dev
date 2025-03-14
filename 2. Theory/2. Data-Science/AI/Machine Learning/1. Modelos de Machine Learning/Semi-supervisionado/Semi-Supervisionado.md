O aprendizado semi-supervisionado combina [[Aprendizado Supervisionado]] e [[Aprendizado Não Supervisionado]]. Ele se torna útil em situações onde rotular todos os dados é impraticável (como no aprendizado supervisionado puro) e onde o aprendizado não supervisionado, por si só, não fornece a estrutura necessária.

---
### Exemplo: Transcrição de Mensagens de Voz

Imagine um programa que transcreve mensagens de voz em texto. O aprendizado não supervisionado poderia agrupar palavras por semelhança sonora, mas não entenderia seus significados. Por outro lado, rotular manualmente todos os sons e palavras seria extremamente trabalhoso.

O aprendizado semi-supervisionado oferece uma solução:

1. **Conjunto de Treinamento Menor:** Um conjunto de dados menor, contendo as palavras e frases mais comuns, é rotulado manualmente.
    
2. **Classificações Básicas:** A máquina usa esse conjunto de treinamento para criar classificações básicas, como no aprendizado supervisionado.
    
3. **Expansão do Vocabulário:** A partir das classificações básicas, a máquina analisa os dados não rotulados e expande seu vocabulário usando raciocínio indutivo ou transdutivo.
    

**Raciocínio Indutivo:**

A máquina generaliza a partir dos dados rotulados. Por exemplo, tendo o par "som foto = palavra foto", ela pode inferir a relação entre sons semelhantes e palavras como "fotografia", "fotógrafo", "fotocópia", etc. O feedback humano ("Como está essa tradução?") ajuda a refinar o modelo.

**Raciocínio Transdutivo:**

Considera o contexto dos dados não rotulados. No caso de mensagens de voz, o modelo pode focar em substantivos comuns (pessoas, lugares, coisas, horários, datas) para melhorar suas suposições sobre o conteúdo das mensagens.

### Quando usar o Aprendizado Semi-Supervisionado?

O aprendizado semi-supervisionado é eficaz em cenários específicos:

- Quando a máquina consegue criar grupos úteis com relativa facilidade.
- Quando há muitos dados disponíveis, mas rotular todos eles é impraticável.
- Exemplos: Classificação de páginas web, agrupamento de insetos.    

### Limitações:

- O raciocínio indutivo e transdutivo podem levar a erros.
- É uma solução para problemas específicos e pode não ser aplicável em todos os casos.
- Só é eficaz quando nem o aprendizado supervisionado puro nem o não supervisionado são suficientes.

Em resumo, o aprendizado semi-supervisionado oferece uma abordagem híbrida que aproveita dados rotulados e não rotulados para construir modelos mais robustos em situações onde a rotulagem completa é inviável. Entretanto, é importante estar ciente de suas limitações e usá-lo estrategicamente em problemas adequados.

---
#machine-learning 