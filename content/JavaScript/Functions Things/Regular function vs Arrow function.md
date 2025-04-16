---
title: Regular function vs Arrow function
tags:
  - JavaScript
---

### This
- Với regular function (RF), this phụ thuộc vào các nó được gọi
	- Khi RF được gọi như một method của 1 object, this sẽ ref đến object đó
	- Khi được gọi như một standalone function, this sẽ thì global, hoặc underfined với strict mode
``` js
function regularFunction() {
  console.log(this);
}

regularFunction(); // Trong trình duyệt: in ra `window`

let obj = { method: regularFunction };
obj.method(); // In ra `{ method: [Function: regularFunction] }`
```

- Với Arrow function (AF): nó không tạo ra this riêng của nó, à kế thừa this của scope chứa nó
``` js
let obj = {
  value: 10,
  method: function() {
    let arrowFunction = () => console.log(this.value);
    arrowFunction();
  }
};
obj.method(); // In ra `10`, vì `this` của arrow function là `this` của `method`
```

``` js 
let obj = {
  value: 10,
  method: function() {
    function regularFunction() {
      console.log(this.value);
    }
    regularFunction();
  }
};
obj.method(); // In ra `undefined`, vì `this` trong regular function là `global object`
```
	- phân tích ví dụ trên: method được gọi bằng obj.method(), khi đó this của method là obj, regularFunction() được gọi trực tiếp, khi đó this của nó là global object (undefined với 'strict mode')


### Arrow function không có `arguments`
- argument là một đối tượng chứa tất cả các tham số được truyền vào hàm, nếu muốn sử dụng trong AF, ta cần dùng cú pháp rest
``` js 
function regularFunction() {
  console.log(arguments); // In ra các tham số truyền vào
}

const arrowFunction = (...args) => {
  console.log(args); // Sử dụng rest để thay thế arguments
};

regularFunction(1, 2, 3); // [1, 2, 3]
arrowFunction(1, 2, 3);   // [1, 2, 3]

```