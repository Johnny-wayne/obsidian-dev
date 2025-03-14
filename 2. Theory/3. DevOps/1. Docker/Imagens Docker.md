###### Imagens Docker: Uma Explicação Complicada

**Imagine uma receita de bolo.** A receita contém todos os ingredientes e passos necessários para fazer um bolo perfeito. Uma imagem Docker é como essa receita, mas para um aplicativo.

**O que é uma imagem Docker?**

- **Um pacote completo:** Uma imagem Docker é um arquivo que contém tudo o que um aplicativo precisa para funcionar: código, bibliotecas, ferramentas, configurações, etc.
- **Imutável:** Uma vez criada, uma imagem é imutável. Isso significa que você não pode alterar os arquivos dentro dela.
- **Leve:** As imagens Docker são geralmente menores do que máquinas virtuais tradicionais, pois compartilham o kernel do sistema operacional host.
- **Portátil:** Uma imagem Docker pode ser executada em qualquer máquina com o Docker instalado, independentemente do sistema operacional.

**Como funciona?**

1. **Criação:** Uma imagem é criada a partir de um arquivo chamado Dockerfile. Esse arquivo contém uma série de instruções que descrevem como construir a imagem, como instalar pacotes, copiar arquivos, etc.
2. **Execução:** Quando você executa uma imagem, o Docker cria um contêiner a partir dela. Um contêiner é uma instância em execução da imagem.
3. **Isolamento:** Cada contêiner é isolado dos outros e do sistema host. Isso significa que cada aplicativo tem seu próprio ambiente, o que ajuda a evitar conflitos e a garantir a consistência.

**Por que usar imagens Docker?**

- **Consistência:** Garante que o aplicativo sempre funcione da mesma maneira, independentemente do ambiente.
- **Portabilidade:** Facilita a distribuição e implantação de aplicativos.
- **Escalabilidade:** Permite criar e destruir contêineres rapidamente para atender à demanda.
- **Isolamento:** Protege os aplicativos de problemas em outros contêineres ou no sistema host.

---
##### Simplificando Docker:

- Imagens: Blueprints de programas
- Containers: Instâncias das imagens

Aqui estamos inicializando um container a partir de uma imagem do MongoDB
```yml
version: '3.8'

services:
  db: 
    image: mongo
    container_name: db
    restart: always
    environment: 
      - MONGO_INITDB_ROOT_USERNAME=dio
      - MONGO_INITDB_ROOT_PASSWORD=dio
    ports:
      - "27017:27017"
    volumes:
      - C:/Users/johnn/Desktop/docker-dio/dbdata:/data/db
```

Essa parte define as variáveis do ambiente que precisam ser definidas junto com o Mongo, neste caso, e o usuário e a senha inicial.
```yml
environment: 
      - MONGO_INITDB_ROOT_USERNAME=dio
      - MONGO_INITDB_ROOT_PASSWORD=dio
```

>[!warning] Se der pau falando algo como "*`mkdir: "Users" file exists`*"
>Tenta criar deletar tudo e criar de novo. Além de deixar a pasta `dbdata` fora do diretório que possui o compose.