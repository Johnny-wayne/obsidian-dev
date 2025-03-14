
### Introdução aos Conceitos Básicos do Microsoft Azure

- O que é computação em nuvem
- Responsabilidade compartilhada
- Modelos de nuvem
- Custo de capital versus custo operacional

---

Maioria das paradas são pagas e se precisar calcular, usa a calculadora do Edge.

Acesse, faça o laboratório e depois exclua. 

---
#### Domínio do Objetivo - Parte 1

- Definir computação em nuvem.
- Definir modelos de nuvem, incluindo público, privado e híbrido.
- Identificar os casos de uso apropriados para cada modelo de nuvem.
- Descrever o modelo baseado no consumo.
- Comparar os modelos de preços de nuvem.

- O que é a computação em nuvem?
	- A computação em nuvem é o fornecimento de serviços de computação pela Internet, habilitando inovações mais rápidos, recursos flexíveis e economias de escala.
	
	- Ele é um ambiente virtualizado
	
	- Basicamente são os serviços de uso de data-centers virtualizados, oferecidos por bigtechs

- Quando a computação em nuvem faz sentido para a minha empresa?
	- A questão de você criar recursos de maneira muito rápida já é muito vantajoso. Mas precisa de pessoas capacitadas para usar isso. 
	- Tem empresa que prefere comprar servidor e já era. Mas Startups e empresas grandes, normalmente precisam disso.

Na nuvem tem de tudo:
- Computação
- Rede
- Armazenamento
- etc
- Dá pra criar tudo na nuvem

##### Modelos:

1. Nuvem privada
	- Quando você trabalha com ambiente 100% on-premisse.
	- As organizações criam um ambiente em nuvem em seu datacenter.
	- As organizações são responsáveis por operar os serviços que fornecem.
	- Não fornece acesso aos usuários fora da organização.

2. Nuvem pública
	- Quando os recursos são oferecidos à diversas pessoas.
	- Um bom exemplo, é o próprio Microsoft Azure.
	
	- Pertencente a serviços de nuvem ou provedor de hosting.
	- Fornece recursos e serviços a várias organizações e usuários.
	- Acessada via conexão de rede segura (geralmente pela internet)

3. Nuvem híbrida
	- O melhor dos dois mundos
	- "Temos nossos próprios servidores, mas também precisamos usar de outros provedores"
	- A minha nuvem privada enxerga o que tenho na minha nuvem pública e podemos até comunicar os dois recursos

4. Modelo muti-cloud
	- Quando você tem vários provedores públicos e ainda tem um privado.
	- "Usa AWS, Microsoft, etc e um datacenter privado".

---
#### Comparação de modelos de nuvem - parte 2

1. **Nuvem pública:**
	
	- Nenhuma despesa de capital para escalar verticalmente
		- Nenhuma despesa de capital ou *[[Formação AZ-900#Comparação entre CapEx e OpEx | CapEx]]* é necessária pra você escalar
		- Você paga depois de 30 dias os recursos que você criou/adquiriu
		
	- Os aplicativos podem ser provisionados e desprovisionados rapidamente.
		
	- As organizações pagam apenas pelo que utilizam
	
2. Nuvem privada
	- As organizações têm controle total sobre os recursos e a segurança
		
	- As organizações são responsáveis pela manutenção e pelas atualizações de hardware.
	
3. Nuvem Híbrida
	- As organizações determinam onde executar seus aplicativos.
		- Podemos escolher se queremos criar nos Estados Unidos ou no Brasil, por exemplo.
	- As organizações controlam a segurança, a conformidade e os requisitos legais.
		
	- Fornece a maior flexibilidade.

---
#### Comparação entre CapEx e OpEx
*Despesa de Capital x Despesa Operacional*

- **Despesas de capital (CapEx)**
	- O gasto inicial de dinheiro em infraestrutura física
	- As despesas do CapEx têm um valor que se reduz com o tempo
	É tipo financiar uma casa, depois que tu paga, fica sussa

- **Despesas operacionais (OpEx)**
	- Gastar com produtos e serviços conforme necessário, pagamento conforme o uso.
	- Seja cobrado imediatamente
	
	Tipo água, quanto mais você beber, mais caro a conta no final do mês. E se você não fizer as contas direito, pode tomar um susto.

###### Modelo baseado em consumo

Os provedores de serviços em nuvem operam em um modelo baseado em consumo, o que significa que os usuários finais pagam somente pelos resursos que usam.

- Melhor previsão de custos
- São fornecidos preços para recursos e serviços individuais
- A cobrança é feita com base no seu uso real

Tem bastante ferramentas que auxiliam você a ver os custos.

---
#### Computação em Nuvem - Revisão

- Definir computação em nuvem.
- Definir modelos de nuvem, incluindo público, privado e híbrido.
- Descrever o modelo baseado no consumo.
- Comparar os modelos de preços de nuvem.

---
#### Links úteis

- [https://learn.microsoft.com/training/modules/describe-cloud-compute/2-](https://learn.microsoft.com/training/modules/describe-cloud-compute/2-introduction-cloud-compute)[introduction-cloud-compute](https://learn.microsoft.com/training/modules/describe-cloud-compute/2-introduction-cloud-compute) ​

- [https://learn.microsoft.com/training/modules/describe-cloud-compute/3-what-](https://learn.microsoft.com/training/modules/describe-cloud-compute/3-what-cloud-compute)[cloud-compute](https://learn.microsoft.com/training/modules/describe-cloud-compute/3-what-cloud-compute) ​

- [https://learn.microsoft.com/training/modules/describe-cloud-compute/5-define-](https://learn.microsoft.com/training/modules/describe-cloud-compute/5-define-cloud-models)[cloud-models](https://learn.microsoft.com/training/modules/describe-cloud-compute/5-define-cloud-models) ​

- [https://learn.microsoft.com/training/modules/describe-cloud-compute/5-define-](https://learn.microsoft.com/training/modules/describe-cloud-compute/5-define-cloud-models)[cloud-models](https://learn.microsoft.com/training/modules/describe-cloud-compute/5-define-cloud-models) ​

---
#### Exploração lab

Tudo que está em "versão prévia" pode ou não sumir. Ou seja, não tem garantia, ou SLA - *(Service Level Agreement)*

---
### Benefícios da computação em nuvem

- Descrever os benefícios da alta disponibilidade, confiabilidade, previsibilidade, segurança, governança e capacidade de gerenciamento da nuvem.

###### **Alta disponibilidade**

- Eles vão te dar uma garantia de um certo tempo de disponibilidade do serviço .

- SLA = Contrato de quanto tempo ele pode ficar indisponível ou disponível. 
	- Normalmente acordam uma porcentagem de 99%, 99.9% e 99.95% de disponibilidade. 
	- Se tiver menos do que o acordado no SLA, o provedor, no caso, a Microsoft, vai devolver uma certa quantia do valor, proporcional ao quanto de indisponibilidade ele teve de diferença em relação ao acordado no SLA.

- Um modelo de 99% de disponibilidade pode ficar indisponível por 1.68 horas por semana ou até 7.2 horas por mês, por exemplo.

A alta disponibilidade se concentra em garantir a disponibilidade máxima, independente de interrupções ou eventos que possam ocorrer.

###### **Escalabilidade**

- A escalabilidade refere-se à capacidade de ajustar recursos para atender à demanda.
- A capacidade de escalar significa que você poderá adicionar mais recursos para lidar melhor com o aumento da demanda.

- O outro benefício da escalabilidade é que você não está pagando além do necessário pelos serviços.
- Como a nuvem é um modelo baseado em consumo, você paga apenas pelo que usa.
- Se a demanda cair, você poderá reduzir seus recursos e, assim, reduzir seus custos.

- Com a escala vertical, se você estivesse desenvolvendo um aplicativo e precisasse de mais capacidade de processamento, poderia escalar verticalmente para adicionar mais CPUs ou RAM à máquina virtual.

###### **Escalabilidade**

- Com a elasticidade, se você experimentasse um salto repentino acentuado na demanda, seus recursos implantados poderiam ser expandidos (automaticamente ou manualmente).

- Ex: Black Friday
	- Imagina você precisar aguentar um monte de gente entrando de uma vez no site, mas não saber se vai precisar de tudo aquilo. 

- Por exemplo, você pode adicionar máquinas virtuais ou contêineres por meio da expansão.
- Da mesma forma, se houver uma queda significativa na demanda, os recursos implantados poderão ser reduzidos horizontalmente.

Resumidamente, se precisarmos de mais, pode aumentar automaticamente e se precisarmos de menos, pode diminuir automaticamente.

###### **Confiabilidade**

- Devido ao design descentralizado, a nuvem naturalmente dá suporte a uma infraestrutura confiável e resiliente
- Com um design descentralizado, a nuvem permite que você tenha recursos implantados em várias regiões do mundo.

- Basicamente, se der pau, dá pra consertar bem fácil. 

- Com essa escala global, mesmo que ocorra um evento catastrófico em uma região, as outras regiões ainda estarão em funcionamento.

###### **Confiabilidade**

- A previsibilidade na nuvem permite que você avance com confiança, seja do desempenho ou no custo. Ambas são influenciadas pelo Microsoft Azure Well-Architected Framework

###### **Segurança**

- A nuvem oferece ferramentas de segurança que atendem às necessidades dos clientes mas, é importante lembrar que a implementação de muitas delas devem ser realizadas pelo cliente.

- Segurança, não é responsabilidade do provedor. Não totalmente.

- Se você quiser o controle máximo da segurança, a infraestrutura como serviço fornecerá recursos físicos, mas permitirá que você gerencie os sistemas operacionais e o software instalado, incluindo aplicações de patches e manutenção.

- Se você quiser que a aplicação de patches e a manutenção sejam tratadas automaticamente, as implantações de plataforma como serviço ou software como serviço podem ser as melhores estratégias de nuvem para você.

- Você que teria que atualizar uma máquina, por exemplo.

A Microsoft disponibiliza os serviços, e a gente aplica.

###### **Governança**
*Basicamente, a galera da papelada.*

Como vamos gerir nossos padrões e recursos.

- A auditoria baseada em nuvem ajuda a sinalizar qualquer recurso que esteja fora de conformidade com seus padrões corporativos e fornecem estratégias de mitigação.

- Dependendo do seu modelo operacional, patches de software e atualizações também podem ser aplicados automaticamente, o que ajuda na governança e na segurança.

- Padrões de gestão na nuvem

- Ao estabelecer uma presença de governança o mais cedo possível você poderá manter sua presença de nuvem atualizada, protegida e bem gerenciada.

###### **Gerenciabilidade**

- Um dos principais benefícios da computação em nuvem são as opções de capacidade de gerenciamento. Há dois tipos de capacidade de gerenciamento para computação em nuvem que você aprenderá nesta série e ambos trazem excelentes benefícios.

- Podemos criar recursos na nuvem de várias formas.

- Um dos principais benefícios da computação em nuvem são as opções de capacidade de gerenciamento. Há dois tipos de capacidade de gerenciamento para computação em nuvem que você aprenderá nesta série e ambos trazem excelentes benefícios.

O gerenciamento da nuvem diz respeito a gerenciar seus recursos de nuvem. Por exemplo:
- Escalar automaticamente a implantação de recursos com base na necessidade.

- Implantar recursos com base em um modelo pré-configurado, removendo a necessidade de configuração manual.

Dá pra gerenciar o ambiente de nuvem e seus recursos, por exemplo, por:
- Por meio de um portal na Web
- Usando uma interface de linha de comando
- Usando APIs
- Usando o Powershell

---
#### Exploração lab - Criando máquinas virtuais

Cada uma das estratégias que você adotar, vai influenciar na porcentagem do SLA

---
### Tipos de serviço de nuvem

- Tipos de serviço de nuvem
	- IaaS, PaaS e SaaS

- Objetivos:
	- Descrever IaaS, PaaS e IaaS
	- Descrever o modelo de responsabilidade compartilhada
	- Identificar os casos de uso apropriados para cada serviço de nuvem (IaaS, PaaS e SaaS)

##### IaaS - (Infraestrutura como serviço)
*Normalmente o mais comum, no contexto de serviço em nuvem*

![[Pasted image 20241119003808.png]]

- Crie uma infraestrutura de TI de pagamento conforme o uso alugando servidores, máquinas virtuais, armazenamento, redes e sistemas operacionais de um provedor de nuvem.

##### PaaS - (Plataforma como serviço)

![[Pasted image 20241119004128.png]]

- Fornece um ambiente para a criação, o teste e a implantação de aplicativos de software, sem foca no gerenciamento da infraestrutura subjacente.

##### SaaS - (Software como serviço)

![[Pasted image 20241119004552.png]]

- Os usuários se conectam e usam aplicativos com base em nuvem pela internet: por exemplo, Microsoft Office 365, email e calendários.

Quanto mais você vai subindo, menos responsabilidade você tem

---
#### Modelo de responsabilidade compartilhada

![[Pasted image 20241119004742.png]]

No local = nosso datacenter físico = responsabilidade toda nossa.

###### Comparação dos tipos de serviço

- IaaS 
	- O serviço de nuvem mais flexível
		- Porque você que personaliza/é responsável a maior parte das coisas
	- Você configura e gerencia o hardware para seu aplicativo

- PaaS
	- Focado no desenvolvimento de aplicativo, banco de dados, entre outros.
	- O gerenciamento de plataforma é realizado pelo provedor de nuvem.

- SaaS
	- Modelo de preço de pagamento conforme o uso.
	- Os usuários pagam pelo software que utilizam em um modelo de assinatura.

---


