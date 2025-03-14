Controlam as versões de um arquivo ao longo do tempo.

- Registra o histórico de atualizações de um arquivo
- Gerencia quais foram as alterações, a data, autor, etc.
- Organização, controle e segurança

##### **Tipos de Sistemas de Controle de Versão (VCS), temos:**

Dentre os Sistemas de Controle de Versão (VCS), temos:

- VCS Centralizado (CVCS)
	- **Ex:** CVS, Subversion

- VCS Distribuído (DVCS)
	- **Ex:** Git, Mercurial

---

**VCS Centralizado (CVCS)**

![[Pasted image 20240801002356.png]]
Nele temos apenas um servidor responsável pelo controle de versão, se ele ficar fora do ar, ou os arquivos dentro dele forem corrompidos, os dados ficam inacessíveis.

**VCS Distribuído (DVCS)**

![[Pasted image 20240801002852.png]]
Cada repositório, ou banco de versão é duplicada localmente, o que torna possível editar aquilo mesmo com o servidor fora do ar.

Clona o repositório completo, o que inclui o histórico de versões.
- Cada clone é um backup
- Possibilita fluxo de trabalho flexível
- Possibilidade de trabalhar sem conexão à rede

---

#### **Git**

##### O que é Git?

Sistema de Versão Distribuído 

- Gratuito e Open Source (Código Aberto)
- Ramificações (branching) e fusões (merging) eficientes
- Leve e rápido

> [!tip] Dica
> Melhor seguir a ordem:
> - `git commit`
> - `git pull`
> - (verificar se tá tudo certo)
> - `git push`

---

#### **GitHub**

Plataforma de Hospedagem de código para controle de versão com Git, e colaboração.
- Comunidade ativa
- Utilizado mundialmente
- Mascote "Octocat"



