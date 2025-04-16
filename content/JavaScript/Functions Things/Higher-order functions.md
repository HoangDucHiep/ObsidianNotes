---
title: Higher-order functions
tags:
  - JavaScript
---

> [!NOTE] what is this?!
> Higher-Order Function là một hàm operate trong một hàm khác, bằng các truyền nó như một biến hoặc được return.

``` js
function greaterThan(n) {
	return m => m > n;
}

let isGreaterThan10 = greaterThan(10);

console.log(isGreaterThan10(3));
console.log(isGreaterThan10(12));
```
