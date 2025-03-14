
#### Instalação
*Instala normalzinho lá*

- **Git Bash** - Terminal do git
- **Git GUI** - *Git Graphic User Interface*

Algumas vezes o git vai precisar usar um editor de texto, como o **Bloco de notas**, **Notepad++**, etc.

Pra descobrir só mandar um:
```
git config --global core.editor
```

**Alternativamente**

Se você quiser ver todas as configurações do Git, incluindo o editor de texto, você pode usar:
```
git config --list
```

#### Configurações Iniciais

Normalmente você configura inicialmente:
- `git config --global user.name Name-example`

- `git config --global user.email emailexample@gmail.com`

- `git config --global init.defaultBranch main`  - *se não der, tenta `init.defaultbranch`*

--- 
#### Autenticação

##### Via Token

Antigamente era feito só com o nome de usuário e com a senha
Depois veio a autenticação por dois fatores

###### **Características**
- **Único** - Tokens are specific to Github and can be generated per use or per device
- **Revocable** - Tokens can be individually revoked at any time without needing to update unaffected credentials
- **Limited** - Tokens can be narrowly scoped to allow only the access necessary for the use case
- **Random** - Tokens are not subject to the types of dictionary or brute force attempts that simpler passwords that you need to remember or enter regularly might be

###### **Passos**

1. Criar um repositório privado
2. Add READ.ME
3. Tenta clonar sem estar autenticado `git clone URL`
4. Ele vai pedir o nome de usuário (coloca a do GitHub mesmo)
5. Ele vai pedir a senha 
	- Se colocar a do GitHub, vai dar erro, falando que a autenticação com senha foi desabilitada em 13 de Agosto de 2021
	- E aí vai falhar
6. Pra realizar a autenticação você vai precisar
	- Criar um novo token
	- Configurar o token 
		- Descrição
		- Tempo pra expiração
		- Definir os limites de escopo do Token
		- Copia o código antes de sair da página
	- Cola no lugar da senha
7. E pronto

###### Bônus

Pra não precisar salvar o token por motivos de segurança, se a gente precisar fazer um clone ou algum processo que precise de autenticação, a gente pode estar salvando as credenciais na nossa máquina.

Temos duas opções:
- `git config --global credential.helper cache` - salva temporariamente - *(recomendado em casos de vários usuários na máquina)*
- `git config --global credential.helper store` - salva na permanentemente - *(recomendado em caso de uso único)*

1. Pra saber em qual tá configurado:
	- `git config --global credential.helper`
	- Aí retorna  `store` ou `cache` normalmente

2. Pra saber aonde ele tá configurada:
	- `git config --global --show-origin credential.helper`
	- ex de resposta: `file:C:/Users/Flitz/.gitconfig store`

3. Pra acessar essa pasta,
	1. verifica se o caminho do CLI é `~`, e lança um:
	- `cat gitconfig`
		Aí vai aparecer o email do usuário, o nome, a branch padrão e a credencial (`credential.helper`) usada, nesse caso é `store`

No mesmo arquivo `file:C:/Users/Flitz/.gitconfig store`, ele tem a credencial armazenada, só dar um
- `cat .git-credential` 
- Ex: `https://eliodiana:ghp_5k35A09KrMiAmgzLtwwwY3iBbTmhqq1ZdbY4@github.com`

> [!tip] Dicona
> Se você é um usuário antigo e entra sem pedir token, deve ser pq você já tem essas credenciais salvas na sua máquina, e pra colocar o token você precisa tirar elas
> - Entra no ***Gerenciar Credencias do Windows*** e aí você vai lá e remove a credencial referente ao GitHub

--- 

##### Via chave [[SSH]]
*SSH - Secure Shell*

De maneira simplista, é um protocolo de rede que possibilita seu computador local e o servidor remoto (que no caso é o GitHub), se comuniquem de forma segura e criptografada por meio da internet.

##### Passos

1. Config do Repo
2. SSH and GPG keys
3. Abra o Git Bash
4. Verificando se há SSH keys
	- `$ ls -a ~/.ssh`
		- `ls`: listar
		- `-a` ou `-al`: listar todos
5. Cole o comando:
	-  `$ ssh-keygen -t ed25519 -C "you_email@example.com"`
		- `ssh-keygen` - É ele que vai gerar a chave a criptografia
		- `-t` Determinar o tipo do algoritmo
		- `ed25519` - Tipo do algoritmo
		- `-C` - Pra adicionar o comentário que vai identificar qual a funcionalidade, mas nesse caso vai ser o proprietário da chave
		- `"endereçoDeEmail@dogithub.com"` - o comentário com nome do proprietário da chave
6. Coloque o lugar pra salvar a chave (Enter to default file path)
7. Coloque uma ***passphrase*** (Frase secreta pra utilizar como senha)
	- Aqui já criou a chave pública e a privada
	- Agora a gente vai adicionar a chave privada ao SSH Agent
8. Insira o comando:
	- `eval "$(ssh-agent -s)"` - Serve pra startar o SSH Agent
		- `eval` - comando interno do Bash
	- `ssh-add ~/.ssh/id_ed25519` - Joga a chave privada pro agente
9. Colocando a chave pública pro GitHub
	- Coloca o título
	- Coloca o tipo de chave (nesse caso, é autenticação)
	- Agora vamos colar a chave pública
		- Pra isso, roda:
			- `cd ~/.ssh` e depois `ls` pra listar as chaves (lembrando que a pública termina com `.pub`)
			- `cat id_ed25519.pub` aí ele vai exibir o conteúdo da chave, e vamos colar ela no GitHub
10. Clonando usando a chave SSH
	- `git clone git@github.com:perfildogithub` 
	- Aí ele vai perguntar se quer mesmo e vai perdir a *passphrase*
	- E pronto


---
Preguiça de explicar
![[Pasted image 20240813145759.png]]

---
#### Clonando

- `git clone URL` - basicão
- `git clone URL nomeQueQuerDar` - basicão tb
- `git clone URL --branch nomeDaBranch --single-branch` - vai clonar só essa branch, caso contrário, ele vai clonar da `main` ou da `master`

---
#### Desfazendo cagadas

- `rm -rf .git` - remover recursivamente à força um diretório .git na pasta que vc criou sem querer
- `git restore <file>` - restaurando um arquivo apagado pro seu estado antigo
- `git commit --amend -m "mensagem certa"` - Alterando a mensagem do último commit
	- Se você não colocar o traço, ele vai abrir o editor. Aperta primeiro o `i` e aí vai dar pra editar. Pra você sair vc vai apertar `esc` e depois escrever `:wq` 
- `git reset` - Desfazendo commits
	- `git reset --soft <hashDoCommit>`
		- Ele pega os commits posteriores ao que indicamos pela Hash, e coloca em [[staging area]]
	- `git reset --mixed <hashDoCommit` 
		- É o comportamento padrão, ou seja, o mesmo que  `git reset`, o `--mixed` coloca os commits posteriores para a árvore de trabalho, colocando eles como ***untracted***
	- `git reset --hard <hashDoCommit>` 
		- Ele ignora completamente os commits posteriores e desfaz eles, dentro da pasta.
		
---

#### Lidando com Branchs
*Branch = "Ramo" Ramificação do projeto* 

- É um ponteiro móvel para um commit no histórico do repositório

- Quando você cria uma nova Branch a partir de outra existente, a nova se inicia apontando para o mesmo commit da Branch que estava quando foi criada

- `git checkout -b teste` - git saí da branch atual e vai pra nova branch *teste*
- `git chekout main` - saí e vai pra main
- `git branch -v` - mostra o último commit de cada branch

- Caso quisermos que as alterações que fizemos na branch ***(teste)*** apareçam lá na branch ***(main)*** nós vamos precisar mesclar elas.

- `git merge teste` - Lembrando que neste caso, estamos na branch ***(main)***
- `git branch` - lista as branch's que temos
- `git branch -d teste` - deleta a branch

- `echo "#commit-3-branch-teste" > commit-3-branch-teste.txt`
	- **`echo`:** Este é um comando comum em sistemas operacionais tipo Unix (como Linux e macOS). Sua função principal é exibir na tela (stdout) o texto que vem após ele.
	- **`"#commit-3-branch-teste"`:** Esta é a string de texto que o comando `echo` irá exibir. O símbolo `#` geralmente indica um comentário em scripts, mas aqui ele faz parte da string que será escrita no arquivo.
	- **`>`:** Este símbolo é um operador de redirecionamento. Ele redireciona a saída padrão (stdout) de um comando para um arquivo.
	- **`commit-3-branch-teste.txt`:** Este é o nome do arquivo onde o texto será escrito. Se o arquivo não existir, ele será criado. Se ele já existir, o conteúdo existente será sobrescrito.
	
	**O que o comando faz:**
	
	1. O comando `echo` pega a string `"#commit-3-branch-teste"`.
	2. Em vez de exibir essa string na tela, o operador `>` redireciona essa saída para o arquivo `commit-3-branch-teste.txt`.
	3. O conteúdo da string é então escrito no arquivo, sobrescrevendo qualquer conteúdo anterior.
	
	**Em resumo:**
	
	Esse comando cria um novo arquivo (ou sobrescreve um existente) chamado `commit-3-branch-teste.txt` e insere a linha de texto `"#commit-3-branch-teste"` nesse arquivo.

---
#### Conflitos de Merge

###### **O que é um conflito de merge?**

Em sistemas de controle de versão como o Git, um conflito de merge ocorre quando duas ou mais ramificações (branches) fazem alterações em um mesmo arquivo e essas alterações não podem ser automaticamente combinadas. Isso geralmente acontece quando duas pessoas editam a mesma linha de um arquivo ou quando uma pessoa exclui um arquivo e outra pessoa o modifica.

###### **Por que ocorrem?**

- **Alterações concorrentes:** Quando duas ou mais pessoas fazem alterações em um mesmo arquivo ao mesmo tempo.
- **Histórico de ramificações divergentes:** Quando duas ramificações evoluem independentemente por um longo período e acumulam muitas diferenças.

###### **Como identificar um conflito de merge?**

- **Mensagens de erro:** O sistema de controle de versão geralmente informa sobre o conflito durante o processo de merge.
- **Marcadores de conflito nos arquivos:** Os arquivos em conflito terão marcadores especiais (geralmente <<<, === e >>>) indicando as diferentes versões de cada linha.

###### **Como resolver um conflito de merge?**

1. **Identificar os arquivos em conflito:** Use os comandos do seu sistema de controle de versão para listar os arquivos com conflitos.
2. **Editar os arquivos manualmente:** Abra os arquivos em um editor de texto e resolva as diferenças entre as versões.
3. **Marcar o conflito como resolvido:** Use os comandos do seu sistema de controle de versão para informar que o conflito foi resolvido.
4. **Commitar as alterações:** Faça um commit para registrar a resolução do conflito.

**Exemplo de um arquivo com conflito:**

```
<<<<<<< HEAD
Este é o texto da versão A.
=======
Este é o texto da versão B.
>>>>>>> branchB
```

###### **Resolvendo o conflito:**

Você precisará escolher qual versão manter ou criar uma nova versão combinando as duas. Por exemplo:

```
Este é o texto combinado das versões A e B.
```

###### **Ferramentas para resolução de conflitos:**

- **Editor de texto:** A maioria dos editores de texto possui recursos para ajudar na resolução de conflitos, como mostrar as diferenças entre as versões lado a lado.
- **Ferramentas visuais:** Algumas ferramentas de controle de versão oferecem interfaces gráficas para facilitar a visualização e resolução de conflitos.

###### **Prevenindo conflitos de merge:**

- **Revisões frequentes:** Faça commits com frequência para manter as ramificações sincronizadas.
- **Comunicação:** Comunique-se com outros desenvolvedores para evitar trabalhar nos mesmos arquivos ao mesmo tempo.
- **Estratégia de branching:** Use uma estratégia de branching bem definida para minimizar o número de conflitos.
- **Rebase:** Em alguns casos, o rebase pode ajudar a simplificar o histórico de commits e reduzir o número de conflitos.

**Em resumo:**

Os conflitos de merge são uma parte normal do desenvolvimento de software colaborativo. Ao entender as causas e as técnicas de resolução, você pode lidar com eles de forma eficiente e evitar atrasos no seu projeto.



---
### Comandinhos interessantes

- `git log` - informações de alterações e commits
- `echo arquivo/ > .gitignore` - ignora tal arquivo
- `touch aulas/.gitkeep` - cria um arquivo `.gitkeep` dentro da pasta `aulas`
	- `.gitkeep` - É uma convenção para salvar diretórios vazios
- `git reflog` - é um `git log` com mais detalhes
- `git push -u origin main` - 
	- `git push` - Empurra as alterações pro repositório remoto
	- `-u` - Abreviação de `--set-upstream`. Serve pra configurar a branch `main` do repositório remoto (que chamaremos de `origin`, nesse contexto), como a branch `--up-stream` do nosso repositório local. 
		- Basicamente ele vai ligar a branch main remota com a branch main local.
- Tecla `.` no GitHub, abre o editor de código

- `git pull` = `git fech` (baixa as alterações) + `git merge` (junta as alterações)
	- `git fetch origin main` - baixa as alterações
	- `git diff main origin/main` - pega as diferenças da branch local e remota
		- `git diff` - Quais são as diferenças
		- `main` - da branch main (local)
		- `origin/main` - com a da branch remote ***(main)***
			
		- ==Fica mais ou menos nesse formato depois:==
			```
			diff --git a/arquivo.md b/arquivo.md
			new file mode 100644
			index 0000000..1473af2
			--- /dev/null
			+++ b/arquivo.md
			@@ -0,0 +1 @@
			+mensagem da branch.
			```
	- `git merge origin/main` - junta com a branch ***(main)*** do repositório remoto
- `git stash` - arquivar mudanças
	- Sla, achei meio nada a ver, se quiser depois pesquisa mais obre