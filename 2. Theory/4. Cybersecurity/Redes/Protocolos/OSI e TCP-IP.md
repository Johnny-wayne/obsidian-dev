*OSI e TCP/IP*

São modelos conceituais que servem pra descrever, de abstrata, como os dados são transmitidos por uma rede. 

Cada modelo é descrito por uma "pilha" de camadas, assim chamada, porque cada camada é dependente de suas camadas adjacentes, ==você desce na pilha ou sobe na pilha==.

![[OSI e TCP.canvas|OSI e TCP]]

Na parte inferior da pilha está a eletricidade, zeros e uns, e símbolos, aquelas unidades quintessenciais da eletrônica moderna; no topo da pilha estão belas imagens e rich text no seu navegador e cliente de e-mail.

Dados que descem na pilha (enviando dados) passam por **encapsulamento**, onde cada camada de informação é encapsulada em detalhes adicionais e passada para a próxima. Essas informações adicionais normalmente assumem a forma de cabeçalhos e/ou trailers – detalhes adicionados ao início ou fim das unidades de dados recebidas da camada anterior. Uma vez totalmente encapsulados e enviados pelo fio para o sistema de destino, esses dados são movidos de volta para cima na pilha, passando por desencapsulamento, onde cada camada interpretará e removerá (retirar) essas informações adicionais até que apenas os dados originais permaneçam. 

A pilha OSI tem 7 dessas camadas e a pilha TCP/IP tem 4. No entanto, depois que você conhece uma, você basicamente conhece a outra.

## O modelo OSI

O modelo OSI tem 7 camadas. As 4 inferiores são chamadas de camadas de ***“mídia”*** e compreendem as construções mais importantes para endereçamento, transporte de dados e entrega de dados. As 3 camadas superiores são chamadas de camadas de ***“host”*** e dependem do andaime de infraestrutura fornecido pelas camadas de mídia para facilitar a comunicação entre aplicativos.

![[Pasted image 20240804180121.png]]


#### As 7 Camadas OSI

-  **Camada 7 (Aplicação)** - A camada de interação humano-computador. Esta camada lida com os serviços e programas que usam a rede para transmitir e receber dados, como navegadores da web e clientes de e-mail.  
  
  
- **Camada 6 (Apresentação)** - Formatação e apresentação de dados.  Esta camada lida com coisas como compressão/descompressão, criptografia/descriptografia e codificação/decodificação. Basicamente, garante que os dados estejam em um formato utilizável para a próxima camada (Camada 5 se estiver enviando dados, Camada 7 se estiver recebendo).  
  
- **Camada 5 (Sessão)** - Gerenciando sessões de comunicação entre dispositivos - Esta camada é responsável por configurar, manter e derrubar sessões, além de executar funções como autenticação e autorização. Isso garante que as conexões entre clientes sejam abertas pelo tempo necessário para transferir dados e, em seguida, derrubadas assim que a transferência for concluída.  

- **Camada 4 (Transporte)** - Transportando dados entre hosts.  Esta é a camada que lida com portas. Você sabe, como HTTP na porta 80, HTTPS na porta 443. Sendo responsável pela entrega de dados, esta camada também lida com a quebra de grandes transferências de dados em pedaços para entrega e, em seguida, reconstituí-los na outra extremidade. Existem dois protocolos principais que são usados ​​nesta camada: TCP e UDP.  O TCP envia segmentos de dados e tem mecanismos de garantia de entrega, como verificar se há erros nos pacotes, garantir que sejam recebidos na ordem correta e retransmitir quando os pacotes são descartados. Isso garante uma comunicação de alta fidelidade, mas essas verificações e balanços têm um custo de velocidade. Se você quer velocidade — o nome do jogo ao transmitir mídia, como videogames ou filmes — você usa UDP.  O UDP envia datagramas e não se importa se eles chegam ou não — dispare-os e grite "pegue!" É improvável que alguns pacotes descartados estraguem sua sequência de eliminações, então você pode acabar com essa sobrecarga de verificação de erros para satisfazer sua necessidade de velocidade.  


-  **Camada 3 (Rede)** - Transmitindo dados entre dispositivos em diferentes redes, ou seja, roteamento! Esta é a província dos endereços IP, os endereços lógicos atribuídos aos hosts. Já ouviu falar de um roteador? Roteadores são dispositivos de camada 3 que permitem a comunicação entre redes roteando pacotes entre esses dispositivos com base em endereços IP. 


-  **Camada 2 (DataLink)** - Transmitir dados entre nós em uma rede, ou seja, comutação. Esta é a província dos endereços MAC, os endereços físicos atribuídos às placas de rede. Já ouviu falar de um switch? Não o da Nintendo. Switches são dispositivos da Camada 2 que permitem a comunicação em uma rede local encaminhando quadros entre esses dispositivos. Já ouviu falar de pacotes? Quadros são como pacotes, mas na Camada 2.  
  

-  **Camada 1 (Física)** - Transmissão de dados por um meio físico, como um cabo ou pelo ar. Os blocos de construção das comunicações entre eletrônicos – sinais elétricos e as várias unidades de dados de baixo nível que eles representam (bits, ou dígitos binários e símbolos).

---
#### Dica:

Embora seja principalmente teórico, você frequentemente ouvirá camadas OSI em referência a dispositivos no mundo das redes. Por exemplo, switches – aqueles dispositivos que conectam computadores em uma rede local – são tipicamente dispositivos de Camada 2. Mas, eventualmente, switches foram construídos com a capacidade de executar roteamento entre várias redes virtuais (VLANs). Lembre-se de que o roteamento é uma atividade de Camada 3 que usa pacotes e é tipicamente a província de roteadores, e então agora se tornou necessário distinguir entre um switch de Camada 2 e um de Camada 3. Você ouvirá essa diferenciação frequentemente – agradeça-nos depois.

Além disso, os firewalls passaram por uma evolução semelhante. Em seus primeiros anos, eles eram simples filtros de pacotes, operando na Camada 3 (Rede). Então vieram os roteadores da Camada 4, que eram capazes de manter o controle de estados ou conexões estabelecidas sobre TCP, uma característica essencial da Camada de Transporte. Hoje em dia, temos firewalls de próxima geração que podem executar filtragem da Camada 7, reforçando ainda mais a necessidade de esclarecer a Camada com a qual o dispositivo é capaz de trabalhar.

Apesar da residência do modelo OSI principalmente na teoria, prometemos que você não conseguirá evitar ver essa pilha refletida nos produtos e protocolos de rede que usar daqui em diante. Poupe-se dos ciclos cerebrais em suas futuras explorações de rede bloqueando isso logo.

---




## O modelo TCP/IP

Em contraste com o modelo teórico OSI, o modelo TCP/IP é um modelo prático que mapeia mais de perto as comunicações em redes modernas. Onde o OSI falhou em ganhar força para implementações práticas, o modelo TCP/IP ganhou a província das comunicações de rede modernas e foi oficialmente implementado como o Internet Protocol Suite, a espinha dorsal da Internet moderna. Você sabe, como IP, aquele protocolo OSI Layer 3 (Network) que lida com o roteamento entre diferentes redes (ou seja, inter-redes)? É meio que um grande negócio.

Dada sua familiaridade com o modelo OSI, é fácil reconhecer este como uma versão praticamente resumida dele. O modelo TCP/IP combina as Camadas OSI 1-2 (Físico, Link de Dados) em uma única Camada 1 (Acesso à Rede) e as Camadas 5-7 (Aplicação, Apresentação, Sessão) em uma única Camada 4 (Aplicação). Ele também renomeia a camada de Rede (3) para Internet, refletindo seu protocolo titular. Isso deixa você com o seguinte:

1. Camada 1: Acesso à rede
2. Camada 2: Internet 
3. Camada 3: Transporte 
4. Camada 4: Aplicação

![[Pasted image 20240804181547.png]]

Na prática, o modelo TCP/IP fornece o seguinte:

1. Forma a base da Internet e de outras redes de grande escala
2. Fornece uma abordagem simplificada e mais prática para comunicações de rede, em relação ao modelo OSI
3. Serve como padrão universal para comunicação de rede, dada sua ampla adoção e implementação por uma grande variedade de dispositivos e aplicativos.

---

### Questões

#### 1. Os modelos OSI e TCP/IP podem ser melhor definidos como:

- [ ] A. Abstrações úteis para descrever a interoperação de protocolos de rede.
- [ ] B. Modelos de banco de dados que descrevem as interações entre serviços em um aplicativo web.
- [ ] C. Representações exatas de como a pilha de rede pode ser organizada.
- [ ] D. Representações desatualizadas de redes no passado.

- Res
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- posta:
	- A

---

#### 2. Em termos dos modelos de rede OSI e TCP/IP, enviar dados de um aplicativo envolve viajar -------- pela pilha em um processo conhecido como --------; receber dados de um aplicativo envolve viajar -------- pela pilha em um processo conhecido como --------- ______.

- [ ] A. para cima, desencapsulamento; para baixo, encapsulamento
- [ ] B. para cima, encapsulamento; para baixo, desencapsulamento
- [ ] C. para baixo, encapsulamento; para cima, desencapsulamento
- [ ] D. para baixo, desencapsulamento; para cima, encapsulamento

- Resposta:
	- C

---

#### 3. Qual camada do modelo TCP/IP corresponde às camadas Física e de Enlace de Dados do modelo OSI?

- [ ] A. Acesso à rede
- [ ] B. Acesso à Web
- [ ] C. Aplicação
- [ ] D. Transporte

- Tesposta:
	- A

---
#### 4. Um colega acabou de informar que está enfrentando problemas com seu Switch de Camada 3. Em qual camada do modelo OSI esse switch opera?

- [ ] A. Físico
- [ ] B. Aplicação
- [ ] C. Rede
- [ ] D. Link de dados

- Resposta:
	- C

---
#### 5. Um firewall simples foi configurado para simplesmente permitir ou descartar pacotes que ele recebe, sem conhecimento de conexões TCP. Em qual camada do modelo OSI esse firewall opera?

- [ ] A. Camada 3
- [ ] B. Camada 4
- [ ] C. Camada 7
- [ ] D. Nenhuma das anteriores

- Resposta:
	- A