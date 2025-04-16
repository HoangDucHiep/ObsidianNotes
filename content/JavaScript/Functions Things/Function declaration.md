---
title: Function declaration
tags:
  - JavaScript
---
### Syntax
``` js
funtion square(x) {
	return x * x;
}
```

### Lưu ý
- Function declaration có hiện tượng [[Hoisting]], do đó code ở ví dụ này vẫn hoạt động bình thường
``` js
console.log("The future says: ", future());

function future() {
	return "You'll never have her";
}
```