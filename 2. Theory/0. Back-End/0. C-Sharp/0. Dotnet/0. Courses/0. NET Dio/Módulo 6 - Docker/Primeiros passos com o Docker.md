
### Realizando o download de imagens

instalando a hello-world image:
```shell
docker pull hello-world
```

Pra verificar se foi instalada corretamente:
```shell
docker images
```

rodar a imagem
```shell
docker run hello-world
```

Mostra os containers em execução:
```shell
docker ps
```
- Com a flag `-a` na frente, você consegue o que aconteceu recentemente, quais containers foram executados recentemente.

---
#### Executando um container

baixar ubuntu image
```
docker pull ubuntu
```

verificar
```
docker images
```

rodar.
```
docker run ubuntu
```
Mas é aqui que entra o pulo do gato. Nada acontece, o container ficar uns segundos e fecha. Enquanto isso, o terminal trava, só libera quando acabar o tempo de execução de container

Aqui estamos criando um novo container, com o tempo de execução de 10 segundos
```
docker run ubuntu sleep 10
```

Se dermos um `docker ps -a` dá pra ver o tempo que ficou e quando foi iniciado.

Se colocarmos um tempo grande demais para um sleep. Podemos chamar um novo acesso remoto e damos um:

```
docker stop jolly wescoff
```
- Esse `jolly wescoff` é o nome que foi automaticamente gerado para o container.
- Em vez de passarmos o nome do container, podemos passar seu id, para para-lo.

Executamos o sistema operacional, mas eu quero um bash para acessa-lo.

Se dermos um `docker help` ele vai nos dar duas flags muitos interessantes:
- `-t --tty` - abre um pseudo-terminal.
- `-i --interactive`  - abre o modo interativo nesse container.

Então executamos um
```
docker run -it ubuntu
```
Aqui ele vai logar como `usuario@iddocontainer` em vez de `usuario@server`.

Se executarmos um:
```
cat /etc/*release*
```
Dá pra ver que estamos no Ubuntu.

Se dermos um exit, ele saí do container, e volta pro server.

---
#### Executando aplicações no container

Como vamos deixar o container ligado de uma maneira que ele desligue apenas quando quisermos.

```
docker run -dti
```
- a flag `-d` faz com que o container seja executado em segundo plano

Queremos abrir o container e realizar a instalação que iremos usar nesse container:
```
docker exec -it 388 /bin/bash
```
- `exec` - o parâmetro `execute` faz com que possamos executar comando em um container que está rodando
- `388` - esse são os três primeiros dígitos do id do container (só são necessários os três primeiros)
- `/bin/bash` - é oq vamos executar, no caso o bash

- aí vamos tentar rodar uma aplicação chamada "nano"
	```
	nano
	```
	
	vai dar ruim e mesmo que tentemos instalar ela...
	```
	apt -y install nano
	```
	Não vai encontrar
	
	
- porque pra isso precisa atualizar as dependências antes:
	```
	apt update
	```
	
	aí depois:
	```
	apt upgrade -y
	```
	
	e aí sim:
	```
	apt -y install nano
	```

A partir de agora temos o nano instalado. E assim conseguimos instalar aplicações dentro do container.

Aí depois saímos do container. Verificamos se está em execução com o `docker ps -a` e se quisermos para-lo nós digitamos `docker stop 388`, faríamos um *Down* no container um *offline* no container.

---
#### Excluindo e nomeando containers

Pra remover containers:
```shell
docker rm 388
```
- No caso `388` são os primeiros dígitos do id do container

Para remover Images:
```shell
docker rmi hello-world
```

Aqui o cara deu um:
```shell
docker run -dti centos
```
- Não tinha imagem localmente, mas o docker foi e procurou nos repositórios e achou, e puxou from `library/centos` e começou a baixar a imagem.

**Nomeando o container:**

```shell
docker run -dti --name Ubuntu-A ubuntu
```
- Aqui `Ubuntu-A` é o nome do container, e e `ubuntu` é o nome da imagem

---
#### Copiando arquivos para o container

Queremos por exemplo copiar alguns arquivos para o container A

Então entramos no container A
```shell
docker exec -ti Ubuntu-A /bin/bash
```

Criamos uma pasta:
```shell
mkdir /destino
```
*Dá um `ls` pra verificar se foi*

No caso, não precisamos executar o bash pra criar esse diretório, podemos mandar um comando por fora com:
```shell
docker exec Ubuntu-A mkdir /destino
```
- aí aproveita e dá um `docker exec Ubuntu-A ls /`

Bom... aqui no nosso caso, não temos o arquivo `.txt` criado, então eu dei um `touch mytextfile.txt` pra criar no root, e dei um `ls` pra verificar.

Se quisermos copiar o arquivo `mytextfile.txt` do `root` para o `Ubuntu-A`:
```shell
docker cp mytextfile.txt Ubuntu-A:/destino
```

Se eu quiser mandar mais de um arquivo, eu posso instalar o zip:
```shell
apt install -y zip
```

depois zipa tudo que for .txt
```shell
zip MeuZip.zip *.txt
```

Agora manda:
```
docker cp MeuZip.zip Ubuntu-A:/destino
```

E depois descompacta:
```
unzip MeuZip.zip
```
vai perguntar se quer substituir o arquivo existente, clicamos em sim.


##### Copiando arquivos do container

Agora vamos fazer ao contrário.

```shell
docker cp Ubuntu:A/destino/MeuZip.zip Zipcopia.zip
```
Indicamos o caminho que está o arquivo e o nome que terá.  E agora foi baixado para o root.

---
#### TAGs

Suponhamos que precisemos baixar uma versão específica de um sistema operacional que queremos. Como o Debian 9.0

```
docker pull debian:9
```
Colocamos `docker pull debian` e na frente, colocamos a tag que queremos

---
#### Criando um container do MySQL

Começamos com um:
```
docker mysql
```

A imagem do MySQL tem algumas variáveis de ambiente próprias que precisam ser definidas.
```
docker run -e MYSQL_ROOT_PASSWORD=Senha123 --name mysql-A -d -p 3306:3306 mysql
```
- Entendendo:
	- `docker run`
		- Roda o container
	- `-e MYSQL_ROOT_PASSWORD=Senha123`
		- `-e` é a tag que define as variáveis de ambiente, e `MYSQL_ROOT_PASSWORD` é a variável de ambiente à qual colocamos como valor `Senha123`
	- `--name mysql-A` 
		- Definimos como nome `mysql-A`
	- `-d`
		- Pra que rode em background
	- `-p 3306:3306`
		- Isso faz definirmos que porta da esquerda (da nossa máquina)  ouvirá, a porta da direita (do container), ou seja, dentro da porta 3306 da nossa máquina, poderemos acessar a porta 3306 do container.
		- `-p` é a flag que nos permite definir as portas
	- `mysql`
		- É a imagem que estamos usando

Aí executamos um bash no mysql
```
docker exec -it mysql-A bash
```

Já dentro do terminal do mysql, vamos criar um novo banco de dados de exemplo no root do mysql
```
mysql -u root -p --protocol=tcp
```
- `-u root`
	- `-u` flag para nos conectarmos ao usuário, `root` é nosso usuário nesse caso.
- `-p protocol=tcp` 
	- Se você der um `docker ps` você consegue ver o protocolo que estamos usando e as portas, nesse caso, é o tcp.

Se estiver falando que não tá dando pra se conectar, com uma mensagem tipo:
`Can't connect to MySQL server on 'localhost:3306' (99)`
Você só roda o mesmo comando dnv.

Agora temos acesso ao banco, e iremos criar um banco de dados
```
CREATE DATABASE aula;
```

Para mostrar os bancos de dados
```
show databases
```

aí saímos do container, e se você der um `ip a`, você vai conseguir ver informação pra krl de rede lá, e o cara mostra que o docker criou um novo dispositivo de rede, e todo os container seguem na mesma faixa de rede sendo separados pela `/` no final

Se você der o comando `docker inspect -a` vai dar mais um monte de informação, até o Ip

---
#### Acessando um container externamente

Basicamente pra acessar de maneira externa, caso não esteja na mesma máquina ou não esteja configurado para um acesso local. Você vai usar um Client do Mysql, fazer a conexão com ip, usuário, senha, porta e etc. E pronto, vc tá dentro.

---
#### Parando e reiniciando um container

Quando paramos um container, com o `docker stop mysql-A` por exemplo. O container para mas fica lá. Se dermos um `docker run --name mysql-B mysql`, ele vai criar outro container. Então pra que ele só volto a rodar, você dá um:
```
docker start mysql-A
```

Alerta: tome cuidado quando for remover um container de banco de dados. Porque você acaba perdendo os dados, tem que exportar os dados. Mas o cara não ensina essa parte.