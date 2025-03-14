## Como servidores funcionam?

Em resumo, um servidor funciona como um computador poderoso que atende às solicitações de outros dispositivos ("clientes") em uma rede.

---
Para entender melhor, imagine um restaurante:

- **Garçons:** São como os clientes, fazendo pedidos (solicitações) ao servidor.
- **Cozinha:** É como o servidor, recebendo os pedidos, processando-os (preparando as refeições) e entregando-os aos garçons (clientes).

---
Em um servidor real, o processo é similar:

1. **Solicitação:** Um cliente (como um navegador da web ou aplicativo) envia uma solicitação ao servidor.
2. **Comunicação:** A solicitação viaja pela rede até o servidor, que a recebe e interpreta.
3. **Processamento:** O servidor executa a ação solicitada, que pode ser:
    - **Buscar e enviar um site:** Um servidor web busca o site solicitado e o envia para o navegador do cliente.
    - **Armazenar arquivos:** Um servidor de arquivos recebe e armazena arquivos do cliente.
    - **Executar programas:** Um servidor de aplicativos executa programas para o cliente, como um banco de dados ou um jogo online.
4. **Resposta:** O servidor envia a resposta de volta ao cliente, que a recebe e a utiliza.

---
###### Tipos de servidores:

Existem diversos tipos de servidores, cada um com funções específicas:

- **Servidor web:** Armazena e entrega sites para navegadores.
- **Servidor de e-mail:** Envia e recebe e-mails.
- **Servidor de arquivos:** Armazena e compartilha arquivos.
- **Servidor de banco de dados:** Armazena e gerencia dados.
- **Servidor de aplicativos:** Executa programas para clientes.
- **Servidor de proxy:** Intermedeia o acesso à internet, fornecendo segurança e anonimato.

---
Detalhes técnicos:

- **Hardware:** Servidores geralmente possuem hardware mais potente que computadores comuns, para suportar alto tráfego e processamento complexo.
- **Software:** Servidores executam softwares específicos para suas funções, como sistemas operacionais, softwares de gerenciamento e aplicativos.
- **Rede:** Servidores se conectam à rede através de interfaces de rede de alta velocidade para garantir comunicação rápida e confiável.

---
**Importância:**

Servidores são essenciais para o funcionamento da internet e de diversas outras redes. Eles fornecem a infraestrutura necessária para que possamos acessar sites, enviar e receber e-mails, armazenar arquivos, utilizar aplicativos e muito mais.

---
**Para mais informações:**

- **O que é um servidor? - Coodesh:** [https://coodesh.com/blog/dicionario/o-que-e-um-servidor/](https://coodesh.com/blog/dicionario/o-que-e-um-servidor/)
- **Como funcionam os servidores? - Dell Explica:** [https://m.youtube.com/watch?v=AsJWIxh84No](https://m.youtube.com/watch?v=AsJWIxh84No)
- **Web Server: O que é e Como Funciona? - Hostinger:** [https://www.hostinger.com.br/tutoriais/web-server](https://www.hostinger.com.br/tutoriais/web-server)

Espero que esta explicação tenha ajudado a esclarecer como os servidores funcionam! Se tiver mais dúvidas, fique à vontade para perguntar

---


## Hardware

Um servidor é uma máquina que fica o tempo todo ligada, sempre fazendo a mesma coisa. Existem vários tipos de servidores, como [[servidores web]], [[servidores de arquivos]], [[servidores de impressão]], etc., sendo que uma única máquina pode rodar simultaneamente vários serviços, dependendo apenas dos recursos de hardware e da carga de trabalho.

De uma forma geral, qualquer PC pode ser usado como um servidor, basta instalar os softwares apropriados. Para tarefas leves, até mesmo máquinas antigas podem prestar bons serviços. Na época em que o [[ADSL]] e outras opções de banda larga começaram a se popularizar, muitos passaram a usar micros 486 e Pentium 1 para compartilharem a conexão, usando o Coyote e outras distribuições minimalistas. Alguns deles ainda continuam funcionando até os dias de hoje, resistindo à passagem do tempo.

Entretanto, quando falamos de [[servidores de hospedagem]] e servidores usados em grandes empresas, o cenário é um pouco diferente. Além de rodarem serviços e aplicativos muito mais pesados, atendendo a centenas de usuários simultâneos, estes servidores realizam tarefas essenciais, de forma que qualquer interrupção em suas atividades pode representar um grande prejuízo, ao contrário de um desktop, onde o usuário pode simplesmente reiniciar depois de uma tela azul, como se nada tivesse acontecido. Um bom servidor deve ser capaz de funcionar por anos a fio, com pouca ou nenhuma manutenção. Além de ser otimizado para um conjunto específico de tarefas, ele precisa ser muito mais estável e confiável do que um desktop típico, o que leva a diferenças nos componentes usados.

Começando do básico, a função de um servidor é disponibilizar serviços ([[HTTP]], [[FTP]], [[DNS]], e-mail, bancos de dados, máquinas virtuais e muitos outros) para um grande número de usuários simultaneamente. De acordo com os serviços usados, determinados componentes são mais importantes do que outros. Um servidor de bancos de dados, por exemplo, depende basicamente do desempenho de acesso a disco em operações de acesso aleatório (um grande volume de pequenas leituras, com setores espalhados por diversos pontos dos discos), o que torna necessário utilizar vários HDs em RAID (em geral é utilizado o modo RAID 5 ou o RAID 6) e uma grande quantidade de [[memória RAM]], usada para cache de disco.

Por outro lado, um servidor destinado a rodar aplicativos, como um [[servidor de acesso remoto]], por exemplo, precisa predominantemente de processamento e memória. O desempenho do HD não é tão importante (pois os aplicativos usados quase sempre já estarão carregados na memória ou no cache de disco), mas um processador com dois (ou quatro) núcleos e muito cache L2 é essencial para rodar o brutal número de processos simultâneos.

Antigamente, era comum o uso de placas com suporte a dois ou quatro processadores, mas com o lançamento dos processadores dual-core e quad-core elas se tornaram menos comuns (já que sai muito mais barato usar um único processador quad-core do que usar uma placa-mãe com 4 processadores separados). Apesar disso, servidores com vários processadores ainda resistem em diversos nichos, agora utilizando processadores AMD Opteron e Intel Xeon com vários núcleos. Juntando quatro processadores AMD Opteron 83xx (quad-core), por exemplo, temos nada menos do que 16 núcleos, o que resulta em uma potência de processamento brutal em diversas tarefas de servidor, onde o desempenho é diretamente limitado pelo volume de processamento disponível.

Diferente de um desktop, onde mesmo um processador dual-core acaba sendo sub-utilizado devido à carência de aplicativos otimizados, servidores como o [[Apache]] trabalham carregando diversas instâncias do serviço a partir do processo principal e são por isso naturalmente otimizados para o uso de diversos núcleos. Um servidor movimentado pode manter centenas de instâncias carregadas simultaneamente, de forma que a carga de trabalho acaba sendo dividida entre os diversos núcleos naturalmente.

Além da questão do desempenho, o servidor precisa ser muito confiável, o que leva ao uso de componentes redundantes. Por exemplo, a maior parte das falhas de hardware são causados por problemas nos HDs ou nas fontes de alimentação. É muito difícil manter um servidor funcionando continuamente por 10 anos (por exemplo) se a vida útil média da fonte é de 3 anos e a do HD é de 4 anos, por exemplo.

Não é possível fazer o HD trabalhar continuamente por 10 anos na base do decreto, mas é possível usar uma controladora [[RAID]] que ofereça suporte a [[hot-swap]] e usar dois HDs em RAID 1, por exemplo. Dessa forma, o servidor pode continuar funcionando depois da falha em um dos HDs e a substituição pode ser feita “a quente”, com ele funcionando. O mesmo pode ser feito com a fonte de alimentação, com o uso de uma fonte redundante, onde temos duas fontes independentes e a segunda é ativada automaticamente em caso de problemas com a primeira.
