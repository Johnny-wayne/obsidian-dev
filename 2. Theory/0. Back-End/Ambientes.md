---
Important:
  - Variáveis de Ambiente
  - Automatização de Testes
  - Tipos de Ambiente
---

O desenvolvimento de um software é um processo extenso que passa por diversas etapas que visam garantir a qualidade e a estabilidade da aplicação. Por exemplo, imagine que você está construindo um site para seu cliente. Quais passos você deve seguir para garantir a funcionalidade deste site, além de construir o projeto? Quais testes serão necessários? Será que está do jeito que o cliente queria?

Para responder todos esses questionamentos, existem vários tipos de ambientes com características próprias que podem ser utilizados de acordo com a necessidade e escolha da pessoa desenvolvedora e da empresa que ela presta o serviço.

Dentre esses diversos ambientes, podemos citar:

- Ambiente de [[#Desenvolvimento]];
- Ambiente de [[#Teste]];
- Ambiente de [[#Homologação]];
- Ambiente de Pré-Produção;
- Ambiente de [[#Produção]].

Com a popularizarção da [metodologia ágil](https://www.alura.com.br/artigos/o-que-e-metodologia-agil), muitas empresas diminuiram a quantidade de ambientes utilizada na produção de um software, sendo os mais comunsos ambientes de Desenvolvimento, Teste, Homologação e Produção.

Nesse artigo, vamos entender o que são esses ambientes e porque eles são importantes no fluxo de trabalho ágil.

---
#### O que são ambientes?

A razão pelo o qual o desenvolvimento de um software é um processo extenso se deve pelo fato de que precisamos confirmar que todo o sistema funciona corretamente para que ele consiga ser publicado.

> Mas como podemos garantir que esse software produzido está exercendo sua funcionalidade de modo correto?

Isso pode ser assegurado através de uma sequência de testes. Por exemplo: testar o código desde seu modo mais simples, como uma função ou condicional, até pontos mais complexos como as integrações que serão feitas com banco de dados.

Deve-se testar também sua performance, infraestrutura, se as [APIs](https://www.aluralingua.com.br/artigos/o-que-significa-api) retornam o resultado que planejamos e dentre outros diversos testes.

Inclusive, existe uma [Pirâmide de Testes](https://cursos.alura.com.br/extra/alura-mais/entenda-a-piramide-de-teste-c206) que nos ajuda a entender quais os principais testes, quando e por que utilizá-los.

> Mas imagina que complicado e demorado seria fazer todos esses testes na sua máquina enquanto se desenvolve todo o software. Né?!

Pois é. Algumas verificações mais demoradas duram horas, e isso atrasaria toda a implementação do programa, visto que a cada commit você teria que parar e esperar o teste ser finalizado.

É exatamente por isso que, ao invés de verificar todos os testes localmente, utiliza-se outro lugar para executá-los, de forma paralela ou após o desenvolvimento.

O local de desenvolvimento, ou sua máquina, o “lugar” onde realizam-se esses testes mais demorados e testes finais antes de subir um software, assim como a aplicação já publicada, são conhecidos por ambientes.

Na sequência, vamos falar um pouco mais sobre como cada um desses ambientes funciona, vamos lá?

---
### Ambientes
#### Desenvolvimento

Quando criamos um novo projeto ou entramos em uma nova equipe, precisamos alterar o código do projeto para adicionar as funcionalidades que combinamos com a equipe. Isso sempre é feito na nossa própria máquina.

Imagina o que aconteceria se durante o desenvolvimento da aplicação você estivesse conectado em um banco de dados compartilhado por toda a equipe de desenvolvimento e alguém faz uma mudança no `schema` do banco de dados. O que aconteceria?

Nesse caso, se a mudança fosse a deleção de uma tabela que você estivesse usando, a sua aplicação, na sua máquina, iria parar de funcionar, porque a sua versão do código ainda faz referência para aquela tabela.

Na nossa máquina, então, é onde o projeto é codificado e atualizado sem se preocupar com possíveis erros, tendo a liberdade de testar as possibilidades de criação. Mas, pra isso, esse ambiente precisa ser isolado do resto da equipe e outras mudanças que eles estão fazendo.

Esse ambiente individual é conhecido como ambiente de desenvolvimento, sendo isolado e sem muitas integrações com ferramentas externas, visto que a pessoa desenvolvedora utiliza sua própria máquina para trabalhar no projeto, sendo o ambiente que ela mais interage e dedica seu tempo. Atualizações e incrementos de features no projeto também são realizadas nessa etapa.

Boa parte dos testes unitários e de integração serão operados nessa etapa durante o processo de desenvolvimento, antes mesmo de passar para os outros estágios de criação do software.

Mas o que fazemos com os tipos de testes que demoram muito para serem executados?

---
#### Teste

Testes mais extensos e específicos podem ser realizados em outros ambientes. Já que, se eles forem executados no seu ambiente de desenvolvimento, a sua produtividade iria ficar comprometida.

Como não queremos que a equipe fique parada por muito tempo esperando os testes rodarem, é natural que esse trabalho seja executado de maneira automática em um local que não atrase ninguém.

O ambiente de teste é o local em que o projeto é testado de maneira manual ou automatizada. Esses testes são feitos para analisar o funcionamento do sistema, verificar a qualidade do produto, ponderar possíveis falhas de operação e segurança, analisar funcionalidades específicas, dentre outras diversas possibilidades.

Nesse ambiente, o código e a infraestrutura do software tendem a ficar o mais próximo possível de sua versão final. Diferentemente do ambiente de desenvolvimento, aqui, já temos mais integrações com ferramentas e infraestrutura similares ao que iremos encontrar no ambiente de produção.

Isso acontece para garantir sua operação correta ao serem realizados os testes conclusivos da aplicação, no ambiente de homologação, e sua posterior publicação, no ambiente de Produção.

É importante que esse estágio seja o mais automatizado possível para que enquanto ocorram verificações (como de integração e validações funcionais), as pessoas responsáveis pelo desenvolvimento possam se manter livres para continuar as implementações e alterações de código em seus ambientes isolados.

Legal, mas será que o (ou a) cliente, que pediu a implementação de uma funcionalidade, deve ter acesso ao ambiente de testes?

---
#### Homologação
*Teste com dados reais*

Esse é o momento em que sua aplicação está mais próxima do produto final, e é aqui que o seu (ou sua) cliente poderá analisar se o software está de acordo com o esperado.

Uma versão beta, prévia do sistema, pode ser lançada para que um grupo seleto de usuários, ainda isolados do consumidor final, possa verificar features assim como migrações de dados e configurações finais para resolver possíveis falhas antes da publicação do projeto.

Vale lembrar que todos os dados utilizados no ambiente de teste eram dados fantasiosos. Então, esse também é o primeiro momento de sua aplicação com dados autênticos.

O ambiente de Homologação (ou Staging), é portanto também um ambiente de teste que se diferencia da etapa anterior por apresentar uma verificação mais próxima do produto final esperado do software, como citado anteriormente.

E depois de tudo isso, e do cliente aprovando o que foi desenvolvido, chegou a hora de liberar uma nova versão do software para o público geral.

---
#### Produção

Agora o usuário tem acesso ao sistema e consegue utilizá-lo. Esta etapa é considerada por muitos o ambiente mais importante pois é onde os testes finais ocorrem com os utilizadores da aplicação.

É nesse momento também que as pessoas podem passar um feedback geral de funcionamento para os desenvolvedores, o que é uma oportunidade para que possíveis implementações possam ser selecionadas e utilizadas na melhoria do software.

E é por isso que nesse ambiente algumas empresas contam com os usuários para testar novas features de suas aplicações através de estratégias de deploy (colocar no ar a aplicação que teve o desenvolvimento concluído). 

---
#### Estratégias de Deploy

É possível utilizar alguns métodos de deploy que servem como uma segunda opção caso seu software precise ser modificado, sem a necessidade de mantê-lo desativado por um longo período de tempo para manutenção. Mas como isso é possível?

Imagine que você deseja testar um novo formato de menu de seu site, e queira modificar algumas cores para verificar a aprovação do público, mas não quer que seu site fique inativo por muito tempo. Para isso, você pode utilizar o método ***Blue-Green Deployment*** (Implantação Azul-Verde, em português).

O método Blue-Green Deployment consiste em utilizar uma metodologia “lado-a-lado” no qual uma cópia de sua aplicação é feita e todo o processo de manutenção e a implementação passa a ser realizada nessa cópia, enquanto o software original mantém-se funcionando normalmente.

Após efetuadas as alterações, o software original é substituído por sua cópia que apresenta as devidas modificações. Dessa maneira, você consegue trabalhar em sua aplicação, sem que isso prejudique o seu usuário.

Outra maneira de fazer isso é recorrer ao método ***Canary Deployment*** (Implantação Canário, em português), ou CI.

Através deste método há a utilização de duas ramificações: uma chamada de _original_, e a outra de _canary_.

Os usuários que apresentam o ramo original continuam a utilizar o aplicativo normalmente com a versão utilizada. Já os usuários que estão no ramo canary (que geralmente é uma porcentagem menor de pessoas), recebem as atualizações e podem testar e apontar feedbacks sobre as mudanças.

Ufa! Vimos até aqui como esses quatro ambientes funcionam. No próximo tópico, iremos detalhar um pouco sobre o fluxo de trabalho com esses ambientes. Bora?!

---
### Fluxo de Trabalho com os Ambientes

> Mas por que é tão importante manter esses ambientes separados e seguir um fluxo de trabalho?

Vamos supor que você passou o dia inteiro construindo a aplicação e fez o commit dela apenas no final do dia, quando todo o seu projeto estava pronto. Por ter ficado apenas em sua máquina, não foi possível realizar alguns testes necessários para concluir que a aplicação estava funcionando corretamente durante esse período. E um desses testes reprovou boa parte da sua criação, o que fez com que você tivesse que refazer todo o processo de codificação no dia seguinte.

Apesar de ser uma prática que pode vir a acontecer, isso gera retrabalho, aumenta o período de desenvolvimento daquele software e pode até mesmo afetar a qualidade de sua aplicação, além de ocasionar uma frustração no time.

É por isso que existem algumas práticas comuns para a pessoa desenvolvedora de software exercer durante esse período de trabalho, conhecida pelo termo _**Continuous Integration**_ (Integração Contínua, em português).

Esse conjunto de práticas tem como intuito introduzir um fluxo de trabalho mais ágil e seguro, na qual o feedback é contínuo e rápido desde o começo do processo de desenvolvimento, o que evita erros maiores no futuro e diminui o tempo de produção do projeto, prezando principalmente pela qualidade e velocidade de geração. Isso indica que muitos dos testes realizados são feitos de uma forma automatizada.

==Há muitos desenvolvedores que preferem utilizar apenas três ambientes em seu processo de criação e focar nas etapas de desenvolvimento, testes e produção da aplicação.==

Isso se deve ao fato de que quanto mais ambientes temos, mais demorado pode ser o processo e maior a chance de ocorrer uma falha, o que pode aumentar o valor financeiro da produção.

A seguir, vamos ver algumas vantagens de manter o Fluxo de Trabalho ágil na construção de um software.

### Vantagens do Fluxo de Trabalho ágil

Como foi falado no tópico anterior, um fluxo de trabalho ágil permite que o tempo de produção de uma aplicação seja menor devido a quantidade de testes automatizados, que preza pela qualidade e velocidade de entrega através de uma cultura de feedback contínuo. Além disso, você sabe quais são as vantagens de manter esse método na criação de um software?

Pois bem, um dos principais pontos é a _**automatização de testes**_, que permite que possíveis bugs sejam encontrados mais rapidamente no processo, o que proporciona a possibilidade de testes adicionais serem executados, além de diminuir a quantidade de trabalhos manuais realizados pela equipe, fazendo com que as pessoas desenvolvedoras possam focar em outros pontos da criação, afora de ficar corrigindo erros reportados anteriormente.

Outro ponto a ser citado é a **_melhora na qualidade e segurança das entregas_**, visto que com testes manuais a quantidade de erros que podem passar despercebidos aumentam, e com a validação automática, o nível de confiabilidade aumenta ainda mais.

Isso garante também uma _maior satisfação dos usuários_, visto que todo o processo se torna mais rápido. Suponha que um usuário ache um erro na aplicação e passe um feedback para a equipe: esse erro poderá ser solucionado mais rapidamente.

Por apresentar testes automatizados e um feedback persistente, o time passa a ter uma _produtividade e desempenho mais elevados_, visto que o processo é realizado de uma maneira mais dinâmica e direta, como [pesquisas realizadas](https://continuousdelivery.com/evidence-case-studies/#research) no assunto afirmam.

Além de todas essas vantagens, podemos citar a famosa expressão de Benjamin Franklin: “Tempo é Dinheiro!”. Pois bem, se nossa aplicação está sendo produzida mais rapidamente e mantendo a qualidade, os custos de produção serão mais reduzidos.

Agora que vimos como ocorre o fluxo de trabalho e as vantagens de utilizarmos um fluxo com Integração Contínua, quais são os riscos de termos diferentes ambientes na construção do nosso Software?

### Cuidados com compartilhamento de informações

Por existir mais de um tipo de ambiente, o fluxo de informações entre eles deve ser feito de um jeito mais cuidadoso possível.

Suponha que você está trabalhando com um banco de dados e utiliza uma chave para esse banco. Ao alterar o ambiente, essa chave não será a mesma para o banco de dados seguinte. Mas, por ela continuar gravada, acaba sendo usada em outro banco e, de forma indevida, substitui a chave correta, o que impossibilita o acesso naquele ambiente.

Esse fluxo de informações sensíveis deve ser meticuloso para que não ocorram vazamentos ou problemas de configuração do sistema. Uma maneira interessante de assegurar a segurança de informações como credenciais de acesso a banco de dados, chaves de APIs, dentre outras, é através das ==variáveis de ambiente==, que servem para armazenar essas informações.

Existem, por exemplo, pacotes de gerenciamento dessas variáveis, como o Dotenv, que é um pacote do [Node.JS](https://www.alura.com.br/artigos/node-js) com essa funcionalidade. Caso tenha interesse de se aprofundar nesse conteúdo, recomendamos a leitura do artigo [Dotenv: gerenciando variáveis de ambiente](https://www.alura.com.br/artigos/dotenv-gerenciando-variaveis-ambiente) sobre o assunto.

## Conclusão

Nesse artigo aprendemos o que são ambientes, como funciona o fluxo de trabalho de criação de um software, assim como as vantagens de um fluxo agilizado, e vimos um pouco sobre estratégias de deploy e os cuidados com o compartilhamento de informações.

Mas não pare por aí! Que tal aprender um pouco mais sobre [Tipos de testes: quais os principais e por que utilizá-los?](https://www.alura.com.br/artigos/tipos-de-testes-principais-por-que-utiliza-los). E aprender um pouco sobre [Como utilizar variáveis de ambiente no PHP](https://cursos.alura.com.br/extra/alura-mais/como-utilizar-variaveis-de-ambiente-no-php-c121).

## Referências

- [Quantos ambientes devemos ter no ciclo de vida do desenvolvimento de software?](https://talkingabouttesting.com/2020/02/01/ambientes-de-desenvolvimento-teste-desempenho-homologacao-pre-producao-producao/)
- [Diferentes ambientes: Development, Testing, Staging e Production](https://klauslaube.com.br/2011/03/07/diferentes-ambientes.html)
- [Test Environments: Differences Between Dev, Staging, Preprod…](https://www.flagship.io/test-environment/)
- [O que é Continuous Delivery?](https://gaea.com.br/o-que-e-continuous-delivery/)
- [Dotenv: gerenciando variáveis de ambiente](https://www.alura.com.br/artigos/dotenv-gerenciando-variaveis-ambiente)
- [Valt by HashiCorp](https://www.vaultproject.io/)