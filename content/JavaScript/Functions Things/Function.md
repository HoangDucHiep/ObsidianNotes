---
title: Function
tags:
  - JavaScript
---
### Function Statement
``` js
function add2Numbers(num1, num2){
	return num1 + num2;
}

console.log(add2Numbers(1, 2));
```


### Parameters Validation
``` js
function getMeanTemp(temperatures) {
     if (!(temperatures instanceof Array)) {
         return NaN;
     }
     let sum = 0;
     for (let i = 0; i < temperatures.length; i++) {
         sum += temperatures[i];
     }
     return sum / temperatures.length;
}
console.log(getMeanTemp(10));       // -> NaN
console.log(getMeanTemp([10, 30])); // -> 20
```

### Scope
``` js
let x = 10;      // global
if (true) { // {} is a block
	let y = 20;  // local to block
	var z = 30;
}
```
- Nested scope
``` js
const hummus = function (factor) {
    const ingredient = function (amount, unit, name) {
        let ingredientAmount = amount * factor;
        if (ingredientAmount > 1) {
            unit += "s";
        }
        console.log(`${ingredientAmount} ${unit} ${name}`);
    }
  
    ingredient(1, "can", "chickpeas");
    ingredient(0.25, "cup", "tahini");
    ingredient(0.25, "cup", "lemon juice");
    ingredient(1, "clove", "garlic");
    ingredient(2, "tablespoon", "olive oil");
};

hummus(2);
```
- Mỗi local scope chỉ có thể "nhìn" lên local scope chứa nó và global scope. (Lexical scoping)

### Function như cũng như các value
- Function không chỉ có thể gọi, nó cũng có thể được gán vào các biến như các giá trị khác
``` js 
let launchMissiles = function() {
  missileSystem.launch("now");
};
if (safeMode) {
  launchMissiles = function() {/* do nothing */};
}
```

### Ways to make function
- [[Function declaration]]
- [[Arrow functions]]


### Closure
- Được tạo ra khi một hàm được khai báo trong 1 hàm khác, nó có thể truy cập đến tất cả các biến của hàm chứa nó tại một instance local binding, cho dù hàm đó đã hoàn thành việc thực thi.
``` js
function wrapValue(n) {
  let local = n;
  return () => local;
}

let wrap1 = wrapValue(1);
let wrap2 = wrapValue(2);
console.log(wrap1());
// → 1
console.log(wrap2());
// → 2
```

``` js
function multiplier (factor) {
	return number => number * factor;
}

let twice = multiplier(2);
console.log(twice(4));
```