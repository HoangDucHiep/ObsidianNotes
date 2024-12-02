---
title: Shadowing
tags:
  - JavaScript
---
## Shadowing
- ***Shadowing***: declare 1 global variable và 1 local variable có cùng tên
``` js
let counter = 100;
console.log(counter); // -> 100
{
    counter = 200;
    console.log(counter); // -> 200
}
console.log(counter); // -> 200
```

``` js
let  counter  =  100;
console.log(counter);  //  ->  100
{
     let  counter  =  200;
     console.log(counter);  //  ->  200
}
console.log(counter);  //  ->  100
```