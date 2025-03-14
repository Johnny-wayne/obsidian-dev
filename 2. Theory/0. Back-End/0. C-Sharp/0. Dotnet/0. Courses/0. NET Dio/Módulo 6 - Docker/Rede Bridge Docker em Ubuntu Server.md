### Rede Bridge no Docker

- **Conceito:** Uma rede virtual criada pelo Docker para isolar os contêineres da rede física do host.
    
- **Funcionamento:** O Docker cria uma interface de rede virtual (bridge) e cada contêiner recebe um endereço IP nessa rede. A comunicação entre os contêineres ocorre dentro dessa rede virtual, sem interferir na rede física do host.
    
- **Por que usar Bridge?**
    
    - **Isolamento:** Cada contêiner tem seu próprio espaço de rede, evitando conflitos de IP e aumentando a segurança.
    - **Gerenciamento:** Facilita o gerenciamento de redes, permitindo criar redes isoladas para diferentes aplicações.
    - **Escalabilidade:** Permite criar redes complexas com múltiplos contêineres e serviços.

**Então, por que mudar para Bridge?**

- **Padrão:** A rede Bridge é o padrão no Docker. Ao criar um contêiner sem especificar uma rede, ele automaticamente é conectado à rede Bridge padrão.
- **Isolamento:** Se você deseja isolar seus contêineres da rede física do host, a rede Bridge é a opção ideal.
- **Gerenciamento:** Ao usar a rede Bridge, você tem mais controle sobre a comunicação entre os contêineres.

**Quando você pode querer mudar o tipo de rede?**

- **Host:** Se você precisa que um contêiner tenha acesso direto a todos os dispositivos e portas da rede física do host, você pode usar a rede Host.
- **Overlay:** Para redes mais complexas e ambientes em cluster, como o Docker Swarm, você pode usar redes Overlay.

**Como mudar para a rede Bridge?**

Geralmente, não é necessário "mudar" para a rede Bridge, pois ela é o padrão. Se você já criou um contêiner e deseja conectá-lo à rede Bridge, pode usar o comando:

Bash

```
docker network connect bridge nome_do_container
```

Use o código [com cuidado](/faq#coding).

**Em resumo:**

A rede Bridge é a opção mais comum e recomendada para a maioria dos cenários ao usar o Docker. Ela oferece isolamento, gerenciamento e flexibilidade para suas aplicações em contêiner.