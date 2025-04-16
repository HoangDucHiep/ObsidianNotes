---
title: Custom Exceptions và Guard Clauses
tags:
  - architectures
  - Full-Stack
---
# **Custom Exceptions và Guard Clauses trong Clean Architecture**

## **1. Custom Exceptions là gì?**
- **Custom Exceptions** là các ngoại lệ (exception) được tạo riêng để xử lý các lỗi nghiệp vụ một cách rõ ràng và có ý nghĩa hơn.
- Giúp phân biệt các loại lỗi khác nhau trong ứng dụng, từ đó dễ dàng xử lý và debug.
- Tránh sử dụng các ngoại lệ chung chung như `Exception` hoặc `ArgumentException`.

---

## **2. Khi nào nên sử dụng Custom Exceptions?**
✔ Khi cần xác định lỗi nghiệp vụ cụ thể (VD: Đơn hàng không hợp lệ, sản phẩm hết hàng).  
✔ Khi muốn có **thông báo lỗi rõ ràng** cho người dùng hoặc hệ thống logging.  
✔ Khi cần phân biệt nhiều loại lỗi khác nhau để có cách xử lý phù hợp.  

🚫 Không nên sử dụng nếu lỗi có thể được kiểm soát bằng cách khác mà không cần ném ngoại lệ.  

---

## **3. Ví dụ về Custom Exceptions**

### **3.1. Tạo một ngoại lệ cho lỗi không tìm thấy sản phẩm**
```csharp
public class ProductNotFoundException : Exception
{
    public ProductNotFoundException(Guid productId)
        : base($"Sản phẩm với ID {productId} không tồn tại.")
    {
    }
}
```
📌 **Khi gọi:**
```csharp
throw new ProductNotFoundException(productId);
```

---

### **3.2. Tạo ngoại lệ cho lỗi số lượng hàng không đủ**
```csharp
public class InsufficientStockException : Exception
{
    public InsufficientStockException(string productName, int requested, int available)
        : base($"Sản phẩm '{productName}' chỉ còn {available} trong kho, không đủ để đặt {requested}.")
    {
    }
}
```
📌 **Khi gọi:**
```csharp
if (requestedQuantity > availableStock)
{
    throw new InsufficientStockException(product.Name, requestedQuantity, availableStock);
}
```

---

## **4. Guard Clauses là gì?**
- **Guard Clauses** là một kỹ thuật giúp **kiểm tra dữ liệu đầu vào** một cách rõ ràng và ngắn gọn ngay đầu phương thức.
- Giúp mã nguồn **dễ đọc, dễ bảo trì**, tránh lồng ghép điều kiện `if` phức tạp.
- Khi dữ liệu không hợp lệ, **ném ra Custom Exception ngay lập tức**.

---

## **5. Khi nào nên sử dụng Guard Clauses?**
✔ Khi có nhiều điều kiện kiểm tra đầu vào cho một phương thức.  
✔ Khi muốn viết code theo phong cách **fail fast** (phát hiện lỗi ngay từ đầu thay vì chạy tiếp).  
✔ Khi cần tránh **nested if statements** (các điều kiện lồng nhau).  

🚫 Không cần dùng nếu chỉ có một điều kiện đơn giản, có thể kiểm tra trực tiếp.  

---

## **6. Ví dụ về Guard Clauses**

### **6.1. Tạo một lớp Helper để sử dụng Guard Clauses**
```csharp
public static class Guard
{
    public static void AgainstNull(object value, string parameterName)
    {
        if (value == null)
            throw new ArgumentNullException(parameterName, $"{parameterName} không thể null.");
    }

    public static void AgainstNegativeOrZero(int value, string parameterName)
    {
        if (value <= 0)
            throw new ArgumentException($"{parameterName} phải lớn hơn 0.", parameterName);
    }
}
```

### **6.2. Sử dụng Guard Clauses trong thực tế**
```csharp
public class Order
{
    public Guid Id { get; private set; }
    public Guid CustomerId { get; private set; }
    public List<OrderItem> Items { get; private set; } = new();

    public Order(Guid customerId, List<OrderItem> items)
    {
        Guard.AgainstNull(customerId, nameof(customerId));
        Guard.AgainstNull(items, nameof(items));
        if (!items.Any())
            throw new ArgumentException("Đơn hàng phải có ít nhất một sản phẩm.", nameof(items));

        Id = Guid.NewGuid();
        CustomerId = customerId;
        Items = items;
    }
}
```
📌 **Lợi ích:**
- Kiểm tra **customerId** và **items** ngay khi khởi tạo đơn hàng.  
- Nếu `items` rỗng, ngay lập tức ném ra lỗi.  
- Tránh các điều kiện `if` lồng nhau trong constructor.  

---

## **7. Kết luận**
| **Đặc điểm**            | **Custom Exceptions** | **Guard Clauses** |
|----------------------|------------------|--------------|
| **Mục đích**        | Xử lý lỗi nghiệp vụ | Kiểm tra dữ liệu đầu vào |
| **Cách sử dụng**    | Ném ra ngoại lệ cụ thể | Kiểm tra và ném lỗi ngay lập tức |
| **Lợi ích**         | Rõ ràng, dễ debug, dễ xử lý lỗi | Code ngắn gọn, dễ đọc, tránh nested if |
| **Ví dụ**           | `throw new ProductNotFoundException(id);` | `Guard.AgainstNull(order, "order");` |

💡 **Sử dụng Custom Exceptions và Guard Clauses giúp mã nguồn dễ đọc, bảo trì, và tránh lỗi nghiệp vụ! 🚀**
