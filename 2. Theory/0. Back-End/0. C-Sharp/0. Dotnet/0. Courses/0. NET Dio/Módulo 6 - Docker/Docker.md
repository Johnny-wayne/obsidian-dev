#### Introdução ao Docker e Containers

##### Modelo Cliente-Servidor

O modelo cliente-servidor é uma estrutura de aplicação que distribui as tarefas e cargas de trabalho entre os fornecedores de um recurso ou serviço, designados como servidores, e os requentes dos serviços, designados como clientes.

- Exemplo:
	- Frontend:
		- Você baixou um aplicativo do seu banco no seu celular, tudo que estiver no seu celular relacionado a isso, a gente chama de Frontend. 
		
	- Backend 
		-  Banco
			- O saldo da sua conta por exemplo, não está no seu celular, ele está no servidor, chamamos isso de backend. 
			- Na hora que clicamos no botão de extrato, é feita uma requisição na internet, até onde está o servidor, o servidor fica ouvindo as requisições, ele procura o saldo usando um software (o backend).
			- Por segurança, o servidor que usa o software e escuta a requisição, não guarda o saldo. Ele fica armazenado em um Storage onde temos vários discos. 
			- Então o servidor vai até esse disco, até o saldo, retorna pro servidor e servidor retorna pro cliente (celular).
			- A galera de infra, é a que cuida desses servidores e desses storages.

D.C = Cloud

##### Cloud

A cloud computing é o acesso sob demanda, via internet, a recursos de computação - aplicativos, servidores (físicos e virtuais), armazenamento de dados, ferramentas de desenvolvimento, recursos de rede e muito mais - hospedados em um data center remoto gerenciado por um provedor de serviços em cloud (Cloud Solution Provider). O CSP disponibiliza esses recursos por uma assinatura mensal ou por um valor **Cobrado conforme o uso.**

![[Pasted image 20241018222334.png]]

Mas... temos um problema. Aqui vai uma questão, uma empresa que aluga um servidor, ela alugar um servidor por completo? 

Não, é aí que entra a virtualização.

---
##### Virtualização

A virtualização utiliza software para criar uma camada de abstração sobre o hardware do computador, permitindo que os recursos de hardware de um único computador (processadores, memória, armazenamento, etc) sejam divididos em vários computadores virtuais. É o tal da Máquina Virtual

Resumidamente, virtualização, é dividir a capacidade de processamento, armazenamento, entre outros, de um servidor físico em partes menores com um software. Basicamente, dividir um servidor completo em servidores menores usando software.

Essa ideia é dos anos 60, mas começou a se popularizar nos anos 90, com o VMware.

- **Diagrama de Virtualização:**
	![[Pasted image 20241018223136.png]]
	
	- Precisamos de um Hardware
	- Um SO (host), no caso, Sistema Operacional (principal). Ex: Windows
	- Um  software chamado de Hypervisor, como o VMware
		- Dentro dele, conseguimos instalar outro sistema operacional, que chamamos de Guest. Ex: Linux
		- Dentro do guest, podemos instalar um banco de dados MySQL e podemos ter uma aplicação PHP
		- Podemos ter outros sistemas operacionais com outros programas junto tb.

Mas aí temos um outro problema. Quando entramos no cenário corporativo, as coisas precisam ser rápidas, os software tem que ser rápidos, e essas máquinas virtuais, às vezes, *não são rápidas o suficiente*. 

A VM resolve uma série de problemas, mas ela ainda é um pouco lenta. Mas e se nós conseguíssemos dividir a máquina virtual em pequenos serviços? 

---
##### Microsserviços

Microsserviços são uma abordagem arquitetônica e organizacional do desenvolvimento de software na qual o software consiste em pequenos serviços independentes que se comunicam usando APIs bem definidas. Esses serviços pertencem a pequenas equipes autossuficientes.

As arquiteturas de microsserviços facilitam a escalabilidade e agilizam o desenvolvimento de aplicativos, habilitando a inovação e acelerando o tempo de introdução de novos recursos no mercado.

Na época do instrutor, tudo era resolvido em um único software, chamado de ***Monolítico***. 

> Hoje, gigantes do mercado como Netflix e Spotify, divulgam a receita do sucesso ao transformar suas aplicações monolíticas em mais de 500 microsserviços.

Quando quebramos uma aplicação monolítica em várias pequenas partes, conseguimos escalá-las de forma separada. Supondo que um serviço de autenticação seja chamado várias vezes durante a sessão de um usuário, com certeza o stress sobre ele é maior

**Por exemplo:**
	Se os caras tão usando o serviço de sacar, demais. Em vez de você duplicar seu programa inteiro pra que ele aguente o tranco, você duplica só o serviço de saque.

Isso é possível graças a tecnologia de container.

---
##### O que é um container

Os contêineres são uma tecnologia usada para reunir um aplicativo e todos os seus arquivos necessários em um ambiente de tempo de execução. Como uma unidade, o contêiner pode ser facilmente movido e executado em qualquer sistema operacional, em qualquer contexto.

---
##### O que é Docker?

Com o Docker, é possível lidar com os containers como se fossem máquinas virtuais modulares e extremamente leves. Além disso, os containers oferecem maior flexibilidade para você criar, implantar, copiar e migrar um container de um ambiente para outro. Isso otimiza as aplicações em nuvem (privada e pública).

É chamado de contêiner, também, por causa dessa imagem.
![[Pasted image 20241018230440.png]]

- Normalmente o Guest nesse caso vai ser Linux, porque é mais enxuto.
- Os microsserviços se conversam
- Podemos ter aplicações multilinguagens
- Nesse caso, temos duas máquinas Guests. Mas se quisermos ter só MySQL em uma e só Python em outra, daria. Dá pra organizar de várias formas.

---
##### Qual a diferença entre a virtualização e os containers?

As duas tecnologias são distintas, porém complementares. Veja uma maneira fácil de distinguir ambas:
- Com a virtualização, é possível executar sistemas operacionais (Windows ou Linux) simultaneamente em um único sistema de hardware.
- Os containers compartilham o mesmo kernel do sistema operacional e isolam os processos de aplicação do restante do sistema. Os containers, Linux são extremamente portáteis, mas devem ser compatíveis com o sistema subjacente. 

Basicamente usamos os containers para potencializar as VMs.