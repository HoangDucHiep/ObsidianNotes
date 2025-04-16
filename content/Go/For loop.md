---
title: For loop
tags:
  - Go
---
``` go
for initialization; condition; post {
	// zero or more statements 
}
```
- optional initialization được chạy trước khi vòng lặp bắt đầu
``` go
// a traditional "while" loop 
for condition { 
	// ...
}
```

``` go
// a traditional infinite loop 
for { 
	// ... 
}
```

``` go
// for range
for _, arg := range os.Args[1:] { 
	s += sep + arg
	sep = " " 
}
```
