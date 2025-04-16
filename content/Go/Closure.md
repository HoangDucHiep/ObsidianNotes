---
title: Closure
tags:
  - Go
---
### 1. Khái Niệm Closure

- **Closure là gì?**  
    Closure là một hàm ẩn danh được định nghĩa bên trong một hàm khác. Nó có khả năng truy cập các biến của hàm cha, kể cả sau khi hàm cha đã kết thúc thực thi.
- **Ứng dụng:**
    - Tạo các hàm tùy biến (factory functions)
    - Quản lý trạng thái nội bộ mà không cần biến toàn cục
    - Tạo callback và các hàm xử lý sự kiện

---

### 2. Ví Dụ Cơ Bản

Giả sử bạn có một biến `x` trong hàm `main`, và bạn định nghĩa một hàm ẩn danh sử dụng biến đó:

``` go
package main

import "fmt"

func main() {
    x := 10
    addX := func(y int) int {
        return x + y
    }

    fmt.Println(addX(5)) // Kết quả: 15

    // Thay đổi giá trị của x
    x = 20
    fmt.Println(addX(5)) // Kết quả: 25 vì closure luôn truy cập giá trị hiện tại của x
}
```

Ở ví dụ trên, hàm `addX` là closure, nó “bắt” biến `x` từ hàm `main`. Khi `x` thay đổi, kết quả của `addX` cũng thay đổi theo.

---

### 3. Closure Trả Về Hàm (Returning Closures)

Closure có thể được trả về từ một hàm, cho phép tạo ra các hàm với trạng thái “ghi nhớ” các giá trị ban đầu:

``` go
package main

import "fmt"

// Hàm multiplier trả về một closure nhân số
func multiplier(factor int) func(int) int {
    return func(n int) int {
        return n * factor
    }
}

func main() {
    timesTwo := multiplier(2)
    timesThree := multiplier(3)

    fmt.Println(timesTwo(4))   // Kết quả: 8
    fmt.Println(timesThree(4)) // Kết quả: 12
}
```

Trong ví dụ này, mỗi lần gọi `multiplier` tạo ra một closure “ghi nhớ” giá trị của `factor` riêng biệt.

---

### 4. Cách Hoạt Động của Closure

- **Phạm vi từ khóa (Lexical Scope):**  
    Closure “nhớ” các biến từ phạm vi nơi nó được định nghĩa, không phụ thuộc vào thời gian thực thi.
- **Bắt Biến (Variable Capture):**  
    Khi closure được tạo ra, nó không sao chép giá trị của biến mà lưu tham chiếu đến biến đó. Do đó, nếu biến thay đổi sau, giá trị trong closure cũng thay đổi.

---

### 5. Lưu Ý Khi Sử Dụng Closure

- **Vấn đề đồng thời (Concurrency):**  
    Nếu sử dụng closure trong môi trường đa luồng (goroutines), hãy cẩn trọng với việc chia sẻ biến để tránh race condition.
- **Hiệu năng:**  
    Closure có thể dẫn đến việc sử dụng bộ nhớ lâu hơn nếu chúng “bắt” một phạm vi lớn các biến không cần thiết.
- **Sử dụng hợp lý:**  
    Dù closures rất mạnh mẽ, hãy sử dụng chúng khi thật sự cần thiết để tránh làm code trở nên khó theo dõi.