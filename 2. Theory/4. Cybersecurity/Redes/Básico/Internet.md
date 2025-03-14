- **ISP:** Internet Service Provider
- **Protocol:** A well-know set of rules and standards used to communicate between machines

#### IP address & DNS

#### **IP:** Internet Protocol
Ex: `174.129.14.120` - ipv6

 Os números do IP, obedecem a uma hierarquia, cada parte do endereço de IP  tradicional representa um conjunto de bits. Juntos, eles somam 32 bits, com 8 bits para cada parte do endereço.
- Os primeiros números identificam o país, e a região do dispositivo
- Depois as sub-redes, e aí os dispositivos
- Essa versão de IP addressing é chamada de `IPv4` 
- Suporta mais de 4 bilhões de endereços

Mas a internet ficou mais popular que o esperado, então eles precisaram criar um novo.
- O IPv6
- Ex: `3FFE:F200:0234AB00:0123:4567:8901:ABCD`
	- Eles usam ao total, 128 bits por endereço e suportam mais de 340 undecillion endereços únicos

#### DNS - Domain Name System

Esses endereços são mó complicados, convenhamos, então pra não precisarmos escrever o IPv4 ou o IPv6 do Google por exemplo, entram os DNS's.

Eles basicamente traduzem URL's para endereços de IP e vice-versa. Então quando digitamos:
- `www.example.com` ele vai traduzir para `174.129.14.120`, por exemplo.

Ou seja:
- Seu dispositivo manda uma requisição pra um servidor DNS, e aí muitas vezes ele manda pra outros servidores DNS essa requisição e eles vão retornando o Endereço IP até chegar no seu dispositivo

Os servidores DNS são conectados em hierarquias distribuídas. Por exemplo: 
- Um servidor DNS em específico, é o fodão pela parte `.org` de uma parte da internet, e ele tem vários outros servidores que ele se comunica, distribui e recebe informações.

Inicialmente, DNS foi feito pra ser Open pra todos, e por ser Open, podem invadir. É oq acontece com o ataque `DNS Spoofing`. Quando um hacker muda o endereço IP associado ao DNS do site, levando ele pra outro ao qual ele substituiu.
- Ex: `Code.com` / `ipv6 - 124.141.14.414`
- Ele vai lá e muda pra: 
- `Code.com` / `ipv6 - 542.523.13.515

Com isso, ele pode se passar pelo site ou algo do tipo, como se fosse o site real.


#### **TCP** - Transmission Control Protocol
*Gerencia o mandar e receber de todos os seus pacotes de dados*

Ele faz a requisição pro servidor do Spotify (por exemplo), e vê se todos chegaram, checando um por um, se todos chegaram ele deixa entregar e pronto. Mas se não, ele pede o que falta pro Spotify, e aí ele vê de novo, e aí se tiver tudo lá ele deixa entregar, se não, ele repete.


#### HTTP & HTML

Como todos os computadores do mundo se comunicam?

- URL - Uniform Resource Locator

Bom, praticamente todos os sites, se comunicam com:

- HTTP - **H**yper**T**ext **T**ransfer **P**rotocol
	É basicamente a linguagem usada pros computadores se comunicarem entre si entre browsers e servidores.
	- Ele é bem direto. A comunicação do seu computador com um servidor web, é basicamente feita a partir de `GET` requests.
	
	- Se nós quisermos por exemplo, pegar a página de login do Tumbler, ele vai basicamente fazer um `GET` ao servidor do Tumbler com algo como `GET /login` ou algum outro documento que quisermos pegar, neste caso, pegamos o código HTML da página de login do Tumbler.
	
	- HTML - Hyper Text Markup Language

Nem sempre estamos só pegando informações `GET`, às vezes, enviamos também, quando enviamos um formulário por exemplo, ou faz uma pesquisa. Nesse caso, nosso computador faz um `HTTP POST request`. 

Quando fazemos login no Tumbler por exemplo, estamos fazendo um `POST` request e depois que logamos ele implementa um cookie que nosso browser vê e agora lembra quem somos.

O cookie é basicamente um Id card, um número, que identifica a gente. Para que toda vez que logarmos dnv no Tumbler, nosso computador mande o "cookie Id", e o servidor saiba que somos, e pense "Ata, é um request daquele cara lá".

Sites seguros impedem os hackers de praticarem Snooping e Tampering criando canais seguros com:
- SSL - Secure Sockets Layer
- TLS - Transport Layer Security 

Eles estão ativados quando vc vê um cadiadinho do lado de `https`
- Https - Hyper Text Transfer Protocol Secure

Quando o site pergunta pro browser, pra ter uma conexão segura, ele primeiro provê um certificado digital, que é um oficial id card, provando que o site é o site que ele diz ser.

Certificados, são publicados por certificate authorities, que são entidades confiáveis que verificam a identidade dos websites e emitem certificados pra eles

---
#### Encryption e Public Keys

A internet é livre/pública, mas muitos dados privados são trocados, como fazemos pra que eles não sejam vistos?

Aí entra a Encryption, embaralhar ou mudar a mensagem, pra esconder o texto original.
Agora Decryption, é desembaralhar a mensagem, pra que ela seja legível.

Um dos mais famosos foi a Caesar Cypher. 
Que foi usada por Júlio Cesar para que se os inimigos capturassem a mensagem, eles não soubessem oq significava. Era basicamente algo tipo:

G + 3 = J

Se o sender e o receiver tem o código que decifra a mensagem (o número que nesse caso é 3), então é chamado de KEY

Key - A secret password for unlocking a message

Ex: 
	Hello - com a key de +5 ficaria encriptada assim:
	MJQQT 
	para decriptar, seria só diminuir por 5

Mas isso aí tem um problema, porque era só ir diminuindo e tentando todas as possibilidades que daria no máximo, 26 tentativas.

Uma solução, seria colocar um valor de soma ou subtração pra cada letra.
Usando uma chave de 10 valores, existiriam 10 bilhões de possíveis soluções. Mas um computador demoraria apenas alguns segundos pra tentar todas as possibilidades.

Então, no mundo moderno, a maioria das chaves usam chaves de 256 bits. Com esse número, mesmo que um cara tivesse centenas de milhares de supercomputadores testando milhões de bilhões de chaves a cada segundo cada um, ainda demoraria trilhões de trilhões de trilhões de anos.

O problema é que os chips dobram o processamento e ficam pela metade  do tamanho a cada ano. 

Quando usam a mesma chave pra encriptar e decriptar, é chamado de ***Symmetric Encryption***, como o Caesar Cypher. Pra compartilhar a mensagem, a chave teria que ser compartilhada por duas pessoas em privado, se não, poderiam interceptar a chave na internet já que ela é publica e acessível.

Em vez disso, computadores usam ***Asymmetric Encryption***. Que contém uma chave publica que pode ser compartilhada com qualquer um, e uma chave privada que não é compartilhada.
	A chave pública, serve para criptografar a mensagem, mas só o computador com acesso a chave secreta é possível descriptografar.



