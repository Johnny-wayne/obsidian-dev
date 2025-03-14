---
Id: 2.0.1.0.A
---


Sua principal função é monitorar automaticamente as alterações nos arquivos do seu projeto e reiniciar o servidor sempre que alguma modificação é salva.

**Por que usar o Nodemon?**

- **Aumento da produtividade:** Imagine ter que reiniciar manualmente o servidor a cada pequena alteração no código. Com o Nodemon, esse processo se torna automático, economizando tempo e esforço.

- **Fluxo de trabalho mais ágil:** Você pode ver os resultados das suas mudanças instantaneamente, facilitando a depuração e o desenvolvimento iterativo.

- **Menos distrações:** Ao eliminar a necessidade de reiniciar o servidor manualmente, você pode se concentrar mais na lógica da sua aplicação.

**Como o Nodemon funciona?**

1. **Instalação:** O Nodemon é instalado como uma dependência global ou local do seu projeto.

3. **Monitoramento:** Após a instalação, você inicia o seu script Node.js através do Nodemon. Ele começa a monitorar os arquivos do seu projeto.

5. **Reinicialização:** Quando uma alteração é detectada, o Nodemon reinicia automaticamente o processo Node.js, aplicando as novas modificações.

---

##### Exemplo de Uso

```bash
# Instalação local
npm install nodemon

# Iniciando o servidor
nodemon app.js
```

Ou 
```Bash
# Instalação global
npm install -g nodemon

# Iniciando o servidor
nodemon app.js
```

Ou ainda
```Bash
# Instalação local como dependência de desenvolvimento
npm install -D nodemon

# npx = Iniciando o pacote localmente (possibilitando a instalação local)
npx nodemon app.js
```

---
### Tópicos relacionados:

- [[B. flag -D]]