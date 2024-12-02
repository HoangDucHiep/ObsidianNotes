---
title: Datatypes
tags:
  - JavaScript
---
- JavaScript có 2 loại datatypes là <span style="font-style:italic; font-weight:bold; color:rgb(184, 123, 234)">primitive (simple)</span> và <span style="font-style:italic; font-weight:bold; color:rgb(184, 123, 234)">complex (composite)</span> 

## Literals
> Là giá trị thể hiện chính nó
``` js
let year = 2004;
let month = 4;
let day = 22;

let name = "Hiep"
// 2004, 4, 22 are literals that represent number
//  Hiep is literal represent string
```

## `typeof` Operator
- Là một unary operator, return ra kiểu dữ liệu của một data
- Possible return values:
```
"undefined"
"object"
"boolean"
"number"
"bigint"
"string"
"symbol"
"function"
```

``` js
let  year  =  1990;
console.log(typeof  year);  //  ->  number
console.log(typeof  1991);  //  ->  number
   
let  name  =  "Alice";
console.log(typeof  name);  //  ->  string
console.log(typeof  "Bob");  //  ->  string
   
let  typeOfYear  =  typeof  year;
console.log(typeOfYear);  //  ->  number
console.log(typeof  typeOfYear);  //  ->  string

function thisIsAFunction()
{
	return 1;
}

console.log(typeof thisIsAFunction);
```