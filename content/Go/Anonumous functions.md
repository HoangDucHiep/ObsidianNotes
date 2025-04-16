---
title: Anonumous functions
tags:
  - Go
---
- Là function không có function name
- Được dùng cho:
	- [[Go/Closure|Closure Implementations]]
	- [[Defer |Defer statements]]
	- Defining a code block to be used with a goroutine 
	- Defining a function for one-time use 
	- Passing a function to another function
``` go
package main

import "fmt"

func main() {
	message := "Greeting" 
	func(str string) { 
		fmt.Println(str) 
	}(message)
}
```