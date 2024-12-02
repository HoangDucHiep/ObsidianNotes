---
title: Object
tags:
  - JavaScript
---

> [!NOTE] <span style="color:rgb(184, 123, 234)">Definition</span>
> <span style="font-style:italic; font-weight:bold; color:rgb(184, 123, 234)">Objects</span> are used to store keyed collections of various data and more complex entities.

- Object được tạo ra với cặp ngoặc nhọn `{...}`, với một ***optional list*** các ***properties***
``` js
let testObj = {};
console.log(typeof testObj);
console.log(testObj)

let testObj2 = new Object();
console.log(typeof testObj2);
console.log(testObj2)
```

## Thêm properties
``` js
let person = {
	name: "Hiep",
	age: 20,
	birthDay: "22/04/2004"
};

console.log(person);

person.phone = "0375368563" // ye, that's a real number :)))
console.log(person);
```

## Xóa properties
``` js

let person = {   // same obj 
	name: "Hiep",
	age: 20,
	birthDay: "22/04/2004"
};

console.log(person);

// use delete
delete person.birthDay;
console.log(person);
```

## Sử dụng multiword property name
``` js

let person = {
	name: "Hiep",
	age: 20,
	birthDay: "22/04/2004",
	"favorite food": "beef jerky", // trailing (hanging) comma
};

console.log(person);
```

- Với các multword property name, ta không thể truy cập bằng ***dot access***, ta cần sử dụng ***square bracket notation***:
``` js
let person = {
	name: "Hiep",
	age: 20,
	birthDay: "22/04/2004",
	"favorite food": "beef jerky", // trailing (hanging) comma
};

//console.log(person.favorite food); error
console.log(person["favorite food"]);
delete person["favorite food"];
console.log(person);
```

- square bracket còn có thể sử dụng với các properties phức tạp, có tính tính toán:
``` js

let key = "apple";

let obj = {
	[key + " pen"]: "value",
};

console.log(obj);
```

### Property value shorthand
``` js
function makeUser(name, age) {
	return {
		name: name,
		age: age,
		// ...
	};
}

let user = makeUser("Hiep", 20);
console.log(user);
```
- Ta thấy tên của properties giống với tên variables, thay vì `name: name`, ta có thể chỉ cần `name`
``` js
function makeUser(name, age) {
	return {
		name,
		age,
		// ...
	};
}

let user = makeUser("Hiep", 20);
console.log(user);
```


### Test tồn tại properties sử dụng `in`
``` js
let user = {
	name: "John",
	age: 30,
}

console.log("name" in user);
console.log("age" in user);
console.log("phone" in user);
```


### Loop qua 1 object
``` js
let user = {
	name: "John",
	age: 30,
}

for (let key in user) {
	console.log("===========");
	console.log(`key: ${key}`);
	console.log(`value: ${user[key]}`);
}
```

### Order của key trong object
- Với các [[Interger properties]] thì được sắp xếp, các kiểu khác thì giữ theo added order
``` js
let codes = {
	"49": "Value 1",
	"41": "Value 2",
	// ...
	"20": "Value 2",
	"1": "Value 2",
}
// Interger properties, sắp xếp tăng dần theo interger
for (let key in codes) {
	console.log(key);
}
```

``` js
let codes = {
	"+49": "Value 1",
	"+41": "Value 2",
	// ...
	"+20": "Value 2",
	"+1": "Value 2",
}
// Interger properties, sắp xếp tăng dần theo interger
for (let key in codes) {
	console.log(+key);
}
```