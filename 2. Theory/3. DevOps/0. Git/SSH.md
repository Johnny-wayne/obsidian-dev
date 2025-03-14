- **SSH:** O protocolo SSH (Secure Shell) é utilizado para conexões remotas seguras, permitindo que você se conecte a um servidor remoto, como um servidor de hospedagem ou um servidor Git, de forma criptografada.

- **Chaves SSH:** As chaves SSH são pares de chaves criptográficas (pública e privada) que são utilizadas para autenticar sua identidade em servidores remotos sem a necessidade de digitar senhas.

- **SSH agent:** O SSH agent é um programa que roda em segundo plano no seu computador e armazena suas chaves SSH na memória. Quando você se conecta a um servidor remoto usando SSH, o SSH agent envia automaticamente sua chave pública para o servidor, que então verifica a sua identidade usando a chave privada correspondente.

**Por que usar um SSH agent?**

- **Conveniência:** Elimina a necessidade de digitar suas senhas repetidamente.
- **Segurança:** As chaves SSH são armazenadas na memória, não em um arquivo, o que as torna mais seguras.
- **Eficiência:** A autenticação é mais rápida, pois as chaves já estão carregadas na memória.

**Como funciona na prática?**

1. **Geração das chaves:** Você gera um par de chaves SSH (pública e privada).
2. **Adição ao agente:** Você adiciona a chave privada ao SSH agent.
3. **Conexão SSH:** Quando você se conecta a um servidor remoto usando SSH, o SSH agent envia automaticamente sua chave pública para o servidor.
4. **Autenticação:** O servidor verifica sua identidade usando a chave privada correspondente.


```bash
# Adicionar a chave privada ao SSH agent
ssh-add ~/.ssh/id_rsa

# Conectar a um servidor remoto
ssh user@example.c
```