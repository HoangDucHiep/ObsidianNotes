---
title: Modules
tags:
  - JavaScript
---

> [!NOTE] !!!
> Tách code thành các file nhỏ gọi là các Module, một module có thể chứa một class hoặc một thư viện các [[JavaScript/Functions Things/Function]] phục vụ cho một mục đích cụ thể

### ES Modules
- Sử dụng 2 từ khóa `export` và `import` 
- Dùng export để định nghĩa một class, function hay binding thuộc vào interface của một module
``` js
const names = ["Sunday", "Monday", "Tuesday", "Wednesday",
               "Thursday", "Friday", "Saturday"];

export function dayName(number) {
	return names[number];
}

export function dayNumber(name) {
  return names.indexOf(name);
}
```

- Để dùng các interface đố trong một Module khác, ta dùng `import`
``` js
import {dayName} from "./dayname.js";
// or like this
//import { dayName, dayNumber } from "./daysInWeek.js";
let now = new Date();
console.log(`Today is ${dayName(now.getDay())}`)
// -> Today is Monday
```

- Ta có thể sử dụng export named default để mặc định rằng module đó chỉ export duy nhất một binding
- Lưu ý Mỗi module chỉ có một export default
``` js
// math.js
// Named export
export function add(a, b) {
    return a + b;
}
export function subtract(a, b) {
    return a - b;
}
// Default export
export default function multiply(a, b) {
    return a * b;
}
```

``` js
// main.js
// Import default export (multiply)
import multiply from './math.js';
// Import named exports (add, subtract)
import { add, subtract } from './math.js';
console.log(add(5, 3));       // Output: 8
console.log(subtract(5, 3));  // Output: 2
console.log(multiply(5, 3));  // Output: 15
```

- Ta có thể import all bằng các dùng `import *`
``` js
// main.js
// Import all
import * as math from './math.js';
console.log(add(5, 3));       // Output: 8
console.log(subtract(5, 3));  // Output: 2
console.log(multiply(5, 3));  // Output: 15
```

### CommonJS Modules
- **CommonJS** là một hệ thống **module** được thiết kế để giúp JavaScript có thể viết theo hướng **module** bên ngoài trình duyệt (chủ yếu dành cho **Node.js**). Mỗi file trong CommonJS được coi là một **module** riêng biệt.

##### **Module Wrapping:**  
Trong **Node.js**, mỗi **module** (tệp) được bọc trong một **function wrapper** cung cấp phạm vi riêng tư. Các biến cục bộ quan trọng được cung cấp:
- `require` – dùng để import **module**
- `module` – đối tượng đại diện cho **module** hiện tại
- `exports` – tham chiếu đến `module.exports`
- `__filename` và `__dirname` – đường dẫn của tệp và thư mục hiện tại

##### **Xuất dữ liệu (`export`)**
``` js
// math.js
function add(a, b) {
    return a + b;
}
module.exports = add; // Export một function duy nhất
```

``` js
// math.js
exports.add = function(a, b) {
    return a + b;
};
exports.subtract = function(a, b) {
    return a - b;
};
```

##### **Nhập dữ liệu (`import`)**
``` js
// main.js
const add = require('./math.js');
console.log(add(2, 3)); // Output: 5
```

``` js
// main.js
const { add, subtract } = require('./math.js');
console.log(subtract(5, 3)); // Output: 2
```