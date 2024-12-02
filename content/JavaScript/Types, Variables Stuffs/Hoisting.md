---
title: Hoisting
tags:
  - JavaScript
---
## Hoisting
> <span style="font-style:italic; font-weight:bold; color:rgb(184, 123, 234)">Hoisting</span> là quá trình mà interpreter di chuyển các declaration của function,variables, classes lên trên cùng của scope của chúng, trước khi code được thực thi

``` js
var height = 180;
console.log(height); // -> 180
console.log(weight); // -> Uncaught ReferenceError: weight is not defined
```

``` js
var height = 180;
console.log(height);    //  ->  180
console.log(weight);    //  ->  undefined
var weight = 70;
console.log(weight);    //  ->  70
```