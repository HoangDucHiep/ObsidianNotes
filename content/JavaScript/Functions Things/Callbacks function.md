---
title: Callbacks
tags:
  - JavaScript
---

> [!NOTE] Định nghĩa👌
> Việc một function được passed as argument vào một function khác và được gọi trong function đó

### Synchronous callbacks
- Hàm được gọi tuần tự theo thứ tự các dòng code.
``` js
let inner = function() {
     console.log('inner 1');
}
let outer = function(callback) {
     console.log('outer 1');
     callback();
     console.log('outer 2');
}
console.log('test 1');
outer(inner);
console.log('test 2');
```

### Asynchronous callbacks
- Bất đồng bộ
``` js
let inner = function() {
	console.log("inner 1");
}

let outer = function(callback) {
	console.log('outer 1');
	setTimeout(callback, 1000) /*ms*/;
	console.log('outer 2');
}

console.log('test 1');
outer(inner);
console.log('test 2');
```

