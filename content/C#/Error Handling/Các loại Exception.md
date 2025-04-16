---
title: Các loại Exception
tags:
  - C♯
---
![[Screenshot 2024-12-09 221825.png]]

### 1. **System.Exception**

- **Mô tả:** Lớp cơ sở cho tất cả các loại exception trong C#.
- **Sử dụng:** Không sử dụng trực tiếp để bắt hoặc ném exception. Thay vào đó, bạn nên sử dụng các lớp con cụ thể.

---

### 2. **System.NullReferenceException**

- **Mô tả:** Ném ra khi cố gắng truy cập thành viên của một đối tượng null.
``` c#
string name = null;
Console.WriteLine(name.Length); // Gây ra NullReferenceException
```
---

### 3. **System.ArgumentException**

- **Mô tả:** Ném ra khi một tham số không hợp lệ được truyền cho phương thức.
``` c#
void SetAge(int age)
{
    if (age < 0) 
        throw new ArgumentException("Tuổi không thể âm.");
}
```

---

### 4. **System.ArgumentNullException**
- **Mô tả:** Ném ra khi một tham số null được truyền vào phương thức nhưng không được phép null.
``` c#
void PrintName(string name)
{
    if (name == null)
        throw new ArgumentNullException(nameof(name), "Tên không được để trống.");
}
```

---

### 5. **System.ArgumentOutOfRangeException**
- **Mô tả:** Ném ra khi tham số nằm ngoài phạm vi hợp lệ.
``` c#
void SetIndex(int index)
{
    if (index < 0 || index > 10)
        throw new ArgumentOutOfRangeException(nameof(index), "Chỉ số ngoài phạm vi.");
}
```

---

### 6. **System.InvalidOperationException**

- **Mô tả:** Ném ra khi trạng thái hiện tại của đối tượng không cho phép thực hiện thao tác.
``` c#
void Start()
{
    if (isRunning)
        throw new InvalidOperationException("Đã bắt đầu trước đó.");
}
```

---

### 7. **System.IndexOutOfRangeException**

- **Mô tả:** Ném ra khi truy cập một chỉ mục vượt ngoài phạm vi của mảng.
``` c#
int[] numbers = { 1, 2, 3 };
Console.WriteLine(numbers[5]); // Gây ra IndexOutOfRangeException
```

---

### 8. **System.FormatException**

- **Mô tả:** Ném ra khi định dạng chuỗi không hợp lệ.
``` c#
string input = "abc";
int number = int.Parse(input); // Gây ra FormatException
```

---

### 9. **System.DivideByZeroException**

- **Mô tả:** Ném ra khi phép chia cho 0.
``` c#
int a = 10, b = 0;
Console.WriteLine(a / b); // Gây ra DivideByZeroException
```

---

### 10. **System.IO.IOException**

- **Mô tả:** Ném ra khi có lỗi xảy ra trong hoạt động nhập/xuất.
``` c#
using (var file = File.Open("nonexistent.txt", FileMode.Open))
{
    // Gây ra IOException nếu file không tồn tại
}
```

---

### 11. **System.NotSupportedException**

- **Mô tả:** Ném ra khi một thao tác không được hỗ trợ.
``` c#
throw new NotSupportedException("Hành động này không được hỗ trợ.");
```

---

### 12. **System.OutOfMemoryException**

- **Mô tả:** Ném ra khi hệ thống không thể cấp phát đủ bộ nhớ.
``` c#
int[] largeArray = new int[int.MaxValue];
```

---

### 13. **System.StackOverflowException**

- **Mô tả:** Ném ra khi ngăn xếp tràn do đệ quy vô hạn.
``` c#
// Khi viết hàm đệ quy không có điều kiện dừng
void InfiniteRecursion() => InfiniteRecursion();
```

---

### 14. **System.TimeoutException**

- **Mô tả:** Ném ra khi một hoạt động vượt quá thời gian chờ.
``` c#
// Khi gọi API hoặc xử lý mạng chậm:
throw new TimeoutException("Thời gian chờ đã hết.");
```

---

### 15. **System.UnauthorizedAccessException**

- **Mô tả:** Ném ra khi không có quyền truy cập tài nguyên.
``` c#
// Khi cố truy cập file mà người dùng không có quyền
File.ReadAllText("C:\\protected.txt"); // Gây ra UnauthorizedAccessException
```

---

### Lưu ý khi xử lý Exception:

1. **Try-Catch-Finally:** Sử dụng khối `try-catch` để bắt và xử lý exception:
    
    csharp
    
    Sao chép mã
    
    `try {     // Code có thể gây lỗi } catch (Exception ex) {     // Xử lý lỗi } finally {     // Dọn dẹp tài nguyên }`
    
2. **Custom Exception:** Khi cần, bạn có thể tạo các exception tùy chỉnh kế thừa từ `System.Exception`.
    
3. **Sử dụng chính xác loại exception:** Tránh sử dụng exception chung (như `Exception`) nếu có loại cụ thể phù hợp. Điều này giúp code dễ hiểu và dễ bảo trì hơn.