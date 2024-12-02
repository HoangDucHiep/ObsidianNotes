---
title: Var vs Let
tags:
  - JavaScript
---
## Var vs Let
- `let` ngăn không cho re-declare lại variable
``` js
	var height = 5;
	var height = 10;// no error
	console.log(height);

	let width = 5;
	let width = 10;
	console.log(width) // SyntaxError: Identifier 'width' has already been declared
	```

- let và const có local scope với cả code block thường, var chỉ có local scope khi ở trong [[Function]]
``` js
let  height  =  200;
{
    let  weight  =  100;
    {
        let  info  =  "tall";
	    console.log(height);  //  ->  200
        console.log(weight);  //  ->  100
        console.log(info);  //  ->  tall
    }
    console.log(height);  //  ->  200
    console.log(weight);  //  ->  100
    console.log(info);  //  ->  Uncaught  ReferenceError:  info  is  not  defined
}
```

``` js
var  height  =  180;
{
         var  weight  =  70;
         console.log(height);  //  ->  180
         console.log(weight);  //  ->  70	
}
console.log(height);  //  ->  180
console.log(weight);  //  ->  70

var  globalGreeting  =  "Good  ";
   
function  testFunction()  {
    var  localGreeting  =  "Morning  ";    
    console.log("function:");
    console.log(globalGreeting);
    console.log(localGreeting);
}
   
testFunction();
   
console.log("main  program:");
console.log(globalGreeting);
console.log(localGreeting);  //  ->  Uncaught  ReferenceError:  localGreeting  is  not  defined

```