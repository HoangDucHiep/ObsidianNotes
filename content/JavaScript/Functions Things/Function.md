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

