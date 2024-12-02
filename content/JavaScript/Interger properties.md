---
title: Interger properties
tags:
  - JavaScript
---

> [!NOTE] Integer properties? What’s that?
> The “integer property” term here means a string that can be converted to-and-from an integer without a change.
> So, `"49"` is an integer property name, because when it’s transformed to an integer number and back, it’s still the same. But `"+49"` and `"1.2"` are not:
>
``` js
// Number(...) explicitly converts to a number 
// Math.trunc is a built-in function that removes the decimal part 
console.log( String(Math.trunc(Number("49"))) ); // "49", same, integer property
console.log( String(Math.trunc(Number("+49"))) ); // "49", not same "+49" ⇒ not integer property 
console.log( String(Math.trunc(Number("1.2"))) ); // "1", not same "1.2" ⇒ not integer property
```