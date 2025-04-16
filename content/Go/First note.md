---
title: First note
tags:
  - Go
---
``` go
package main
import "fmt"

func main() {
	fmt.Println("Hello, BF")
}
```

- Go là compiled language, cần chuyển sang dạng mã máy để chạy
	- Dùng lệnh: `go run filename.go` 

- Go code được organize thành các ***packages***
	- Mỗi Package có thể chứa một hoặc nhiều files
	- Và mỗi source file cũng **cần phải được bắt đầu** bằng <span style="font-weight:bold; color:rgb(184, 123, 234)">package declaration</span>
	- `main` là một package đặc biệt, nó định nghĩa một ***standalone executable program***, không phải là một library.
	  `main function` trong `main package` điểm khởi chạy của chương trình
	- 