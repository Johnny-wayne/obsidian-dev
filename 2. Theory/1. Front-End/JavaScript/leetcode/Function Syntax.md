In JavaScript, there are two main ways to declare a function. One of which is to use the `function` keyword.

##### Basic Syntax

The syntax is:

```javascript
function f(a, b) {
    const sum = a + b;
    return sum;
}
console.log(f(3, 4)); // 7
```

In this example, `f` is the name of the function. `(a, b)` are the arguments. You can write any logic in the body and finally `return` a result. You are allowed to return nothing, and it will instead implicitly return `undefined`

---

##### Anonymous Function

You can optionally exclude the name of the function after the `function` keyword.

```javascript
var f = function(a, b) {
    const sum = a + b;
    return sum;
}
console.log(f(3, 4)); // 7
```

---
##### Immediately Invoked Function Expression (IIFE)

You can create a function and immediately execute it in Javascript.

```javascript
const result = (function(a, b) {
    const sum = a + b;
    return sum;
})(3, 4);
console.log(result); // 7
```

Why would you write code like this? It gives you the opportunity to _**encapsulate**_ a variable within a new _**scope**_. For example, another developer can immediately see that `sum` can't be used anywhere outside the function body.

---

##### Functions Within Functions

A powerful feature of JavaScript is you can actually create functions within other functions and even return them!

```javascript
function createFunction() {
    function f(a, b) {
        const sum = a + b;
        return sum;
    }
    return f;
}
const f = createFunction();
console.log(f(3, 4)); // 7
```

In this example, `createFunction()` returns a new function. Then that function can be used as normal.

---
##### Function Hoisting

JavaScript has a feature called _**hoisting**_ where a function can sometimes be used before it is initialized. You can only do this if you declare functions with the `function` syntax.

```javascript
function createFunction() {
    return f;
    function f(a, b) {
        const sum = a + b;
        return sum;
    }
}
const f = createFunction();
console.log(f(3, 4)); // 7
```

In this example, the function is returned before it is initialized. Although it is valid syntax, it is sometimes considered bad practice as it can reduce readability.

---
##### Closures

An important topic in JavaScript is the concept of _**closures**_. When a function is created, it has access to a reference to all the variables declared around it, also known as it's _**[[lexical environment]]**_. The combination of the function and its enviroment is called a _**closure**_. This is a powerful and often used feature of the language.

```javascript
function createAdder(a) {
    function f(b) {
        const sum = a + b;
        return sum;
    }
    return f;
}
const f = createAdder(3);
console.log(f(4)); // 7
```

In this example, `createAdder` passes the first parameter `a` and the inner function has access to it. This way, `createAdder` serves as a factory of new functions, with each returned function having different behavior.