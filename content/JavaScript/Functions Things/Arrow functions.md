---
title: Arrow functions
tags:
  - JavaScript
---
``` js
let add = (a, b) => {
	return a + b;
}

// if function has only one statement, we can write like this
let multiply = (a, b) => a * b;

console.log(add(1, 2));
console.log(multiply(2, 3));

// if has only oone parameter
let factorial = n => n > 1 ? n * factorial(n - 1) : 1;
console.log(factorial(5)); // -> 120
```

