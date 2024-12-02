---
title: First-Class members
tags:
  - JavaScript
---
- Nghĩa là function có thể được sử dụng như data, nó có thể được chứa trong variable, hay passed as arguments vào một function khác.
``` js
function showMessage(message) {
     console.log(`Message: ${message}`);
}
let sm = showMessage;

sm("This is a message!");
console.log(typeof sm);
```

``` js
function add(a, b) {
	return a + b;
}

function multiply(a, b) {
	return a * b;
}

function operation(operatorFunc = add, firstOperand, seccondOperand) {
	return operatorFunc(firstOperand, seccondOperand);
}

console.log(operation(add, 10, 20)); // -> 30
console.log(operation(multiply, 10, 20)); // -> 200
console.log(operation(function(a, b) { return a - b; }, 10, 20)); // 
```

### Function Expression
``` js
let func = function(a, b) {
	return a + b;
}

console.log(func(1, 2));
```