
##### SSH connection 

Depois de configurar o servidor com os nomes, permissão de conexões SSH e outras coisas como nome e senha. Você vai abrir um terminal em algum outro lugar fora do Ubuntu Server e vai colocar no prompt:

```shell
ssh user@190.121.31.41
```

- `ssh` - Conexão ssh
- `user@` - seleciona o usuário ao qual estamos no conectando no servidor
- `190.121.31.41` - o endereço Ip do servidor

aí ele vai pedir a senha do usuário, e depois de colocarmos, estamos dentro.

```shell
cat /etc/*release*
```

---
#### Instalando Docker
Vale lembrar que estamos usando comandos de instalação para a distribuição *Debian*

Honestamente, é só ir na documentação e colar umas coisas.

download do script de instalação:
```shell
curl -fsSL https://get.docker.com -o get-docker.sh
```

Aí ela vai instalar `get-docker.sh` que é o scrpit, aí dá um `ls` ou `ls -l` pra listar se instalou.

Depois pra instalar:
```shell
sh get-docker.sh
```

E pra verificar se instalou:
```shell
docker version
```

E depois, se quiser ver se tá rodando:
```shell
systemctl status docker
```