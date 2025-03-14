---
aliases:
  - CPU
---
Um processador, ou **CPU** - *(Unidade Central de Processamento)*, é um microchip especializado que acelera, endereça, resolve ou prepara dados, dependendo da aplicação. 

Ele é responsável pelo processamento e execução de programas armazenados na memória principal.

- Os processadores são compostos por três unidades principais: 
	- Unidade de controle (UC) 
		- Varia conforme o [[#Ciclo de clock]]
		- Ela recebe as informações através do **Decodificador de Instruções - (DI)**
			- Ele recebe as informações pelo **Registrador de Informações - (RI)**
				- As informações são recebidas e decodificas pelo *RI*
	- Unidade lógica e aritmética (ULA)
	- Registradores.

A *UC* procura instruções na memória e as decodifica. A *ULA* realiza operações aritméticas e booleanas. Os *[registradores]* são uma memória rápida que armazena informações de controlo e resultados intermédios.

![[Pasted image 20240506211810.png]]

---

A **CPU** pode ser divida em duas categorias funcionais, são elas, as quais podem ser chamadas de unidades:
- Unidade Funcional de Controle
	- Ela está ligada à *UC*
- Unidade Funcional de Processamento
	- Agrupa os *registradores* e a *ULA*


----
##### Outros aspectos

- Frequência de processador (velocidade, clock)
- Cache
- Potência

Os processadores podem ter um ou vários núcleos, sendo chamados de *core* ou *multicore*. Os processadores *Intel* e *AMD* mais modernos têm entre 2 e 10 núcleos de processamento. Os modelos profissionais podem ter ==até 64 núcleos==, o que os torna especialmente eficientes em cálculos complexos e tarefas como renderização e decodificação de vídeo.

O clock padrão (ou base) de um processador é estabelecido pelo fabricante do chip com base em critérios técnicos e de segurança. Este limite garante que a CPU funcione de forma consistente, desde que seja complementada com uma ventoinha (cooler) ou sistema de refrigeração adequado.

--- 
#### Ciclo de Clock

