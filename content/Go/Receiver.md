---
title: Receiver
tags:
  - Go
---
- Trong ngôn ngữ lập trình Go, phần `(d *Developer)` trước tên hàm trong đoạn mã bạn cung cấp được gọi là <span style="font-weight:bold; color:rgb(184, 123, 234)">receiver</span>. Receiver xác định kiểu dữ liệu mà hàm đó được liên kết, cho phép gọi hàm như một phương thức của kiểu dữ liệu đó.
``` go
func (receiver_name Type) methodName(parameters) returnType {
    // Thân hàm
}
```

### Value Receiver
- Sử dụng khi phương thức không cần thay đổi giá trị của instance.
- Thường áp dụng cho các kiểu dữ liệu nhỏ và bất biến.
``` go
type Rectangle struct {
    width, height float64
}

func (r Rectangle) Area() float64 {
    return r.width * r.height
}
```

### Pointer Receiver
- Sử dụng khi phương thức cần thay đổi giá trị của instance.
- Giúp tránh việc sao chép dữ liệu lớn, cải thiện hiệu suất.
``` go
func (r *Rectangle) Scale(factor float64) {
    r.width *= factor
    r.height *= factor
}
```