
### Visão geral

Esta questão pretende ser uma introdução aos _**closures**_ . Em JavaScript, funções têm uma referência a todas as variáveis ​​declaradas no mesmo escopo, bem como a quaisquer escopos externos. Esses escopos são conhecidos como o _**ambiente léxico**_ da função . A combinação da função e seu ambiente é conhecida como um _**closure**_ .

#### Exemplo de fechamento

Em Javascript, você pode declarar funções dentro de outras funções e retorná-las. A função interna tem acesso a quaisquer variáveis ​​declaradas acima dela.

```javascript
function createAdder(a) {
  return function add(b) {
    const sum = a + b;
    return sum;
  }
}
const addTo2 = createAdder(2);
addTo2(5); // 7
```

A função interna `add`tem acesso a `a`. Isso permite que a função externa sirva como uma fábrica de novas funções, cada uma com comportamento diferente.

#### Fechamentos versus classes

Você pode notar que o exemplo acima `createAdder`é muito semelhante a um construtor de classe.

```javascript
class Adder {
  constructor(a) {
     this.a = a;
  }

  add(b) {
    const sum = this.a + b;
    return sum;
  }
}
const addTo2 = new Adder(2);
addTo2.add(5); // 7
```

Além das diferenças na sintaxe, ambos os exemplos de código servem essencialmente ao mesmo propósito. Ambos permitem que você passe algum estado em um "construtor" e têm "métodos" que acessam esse estado.

Uma diferença fundamental é que os closures permitem _**o encapsulamento**_ verdadeiro . No exemplo da classe, não há nada que o impeça de escrever `addTo2.a = 3;`e quebrar seu comportamento esperado. No entanto, no exemplo do closure, é teoricamente impossível acessar `a`. Observe que, a partir de 2022, o encapsulamento verdadeiro é atingível em classes com [sintaxe de prefixo #](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields) .

Outra diferença é como as funções são armazenadas na memória. Se você criar muitas instâncias de uma classe, cada instância armazena uma única referência ao _**objeto protótipo**_ onde todos os métodos são armazenados. Enquanto para fechamentos, todos os "métodos" são gerados e uma "cópia" de cada um é armazenada na memória cada vez que a função externa é chamada. Por esse motivo, as classes podem ser mais eficientes, particularmente no caso em que há muitos métodos.

Diferentemente de linguagens como Java, você tenderá a ver código escrito com funções em vez de classes. Mas como JavaScript é uma linguagem multiparadigma, isso dependerá do projeto específico em que você está trabalhando.

### [

](https://leetcode.com/problems/counter/editorial/?envType=study-plan-v2&envId=30-days-of-javascript#approach-1-increment-then-return)Abordagem 1: Incrementar e depois retornar

Declaramos uma variável `currentCount`e a definimos como igual a `n - 1`. Então, dentro da função de contador, incrementamos `currentCount`e retornamos o valor. Note que, como `currentCount`é modificado, ele deve ser declarado com `let`em vez de `const`.

**Implementação**

---

### [

](https://leetcode.com/problems/counter/editorial/?envType=study-plan-v2&envId=30-days-of-javascript#approach-2-postfix-increment-syntax)Abordagem 2: Sintaxe de incremento pós-fixado

JavaScript fornece uma sintaxe conveniente que retorna um valor e _**então**_ o incrementa. Isso nos permite evitar ter que definir inicialmente uma variável para `n - 1`.

**Implementação**

### [

](https://leetcode.com/problems/counter/editorial/?envType=study-plan-v2&envId=30-days-of-javascript#approach-3-prefix-decrement-and-increment-syntax)Abordagem 3: Sintaxe de decremento e incremento de prefixo

JavaScript também tem uma sintaxe que permite incrementar um valor e _**então**_ retorná-lo. Como o incremento acontece antes do valor ser retornado, precisamos primeiro decrementar o valor inicialmente semelhante à Abordagem 1.

**Implementação**

### [

](https://leetcode.com/problems/counter/editorial/?envType=study-plan-v2&envId=30-days-of-javascript#approach-4-postfix-increment-syntax-with-arrow-function)Abordagem 4: Sintaxe de incremento pós-fixado com função de seta

Podemos reduzir a quantidade de código na Abordagem 2 usando uma função de seta com um retorno implícito.

**Implementação**