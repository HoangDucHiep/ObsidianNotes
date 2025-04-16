---
title: variables
tags:
  - Go
---
``` go
package main

import "fmt"

func main() {
	var i, j int = 1, 2
	k := 3
	c, python, java := true, false, "no!"

	fmt.Println(i, j, k, c, python, java)
}
```

- Một biến chỉ declare chứ không được init thì sẽ được gán `zero value`
	- với number types: `0`
	- với boolean type: `false`
	- với strings: `""`
- constant:
``` go
package main

import "fmt"

const Pi = 3.14

func main() {
	const World = "世界"
	fmt.Println("Hello", World)
	fmt.Println("Happy", Pi, "Day")

	const Truth = true
	fmt.Println("Go rules?", Truth)
}
```

