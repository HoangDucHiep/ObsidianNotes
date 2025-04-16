---
title: function
tags:
  - Go
---
- Basic function
``` go
package main

import "fmt"

func add (x, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(42, 13))
}
```
- Mutiple result
``` go
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```
- Named return values
``` go
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	fmt.Println(split(17))
}
```

### Pass by value
- function parameter là pass by value với một số type như strings, symbols, integers, và decimal numbers
``` go
package main

import "fmt"

func swap (x, y int) {
	a := x
	x = y
	y = a
}

func main() {
	a := 1
	b := 2

	swap(a, b)

	fmt.Println(a)
	fmt.Println(b)
}
```
![[pass_by_value 1.gif]]

### [[Receiver]]

### [[Anonumous functions]]
