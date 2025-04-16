---
title: Entities
tags:
  - Full-Stack
  - architectures
---
> - **Entity** trong **Clean Architecture** là một **đối tượng nghiệp vụ** chứa các **thuộc tính (state)** và **hành vi (behavior)** của hệ thống.
> - Nó **không phụ thuộc vào cơ sở dữ liệu** hoặc bất kỳ framework nào (ví dụ: Entity Framework, Dapper...).
> - **Có thể tồn tại trong cả hệ thống sử dụng cơ sở dữ liệu quan hệ (SQL)** và **các hệ thống không sử dụng CSDL quan hệ (NoSQL, file, API)**.
> - **Entity thường là một phần của domain model**, có thể bao gồm **logic nghiệp vụ bên trong nó** chứ không chỉ là một "class chứa dữ liệu".

---
## **Entity khác gì với bảng trong CSDL?**

|**Tiêu chí**|**Entity trong CSDL (ORM)**|**Entity trong Clean Architecture**|
|---|---|---|
|**Mục đích**|Đại diện cho bảng trong CSDL, chỉ chứa dữ liệu|Đại diện cho đối tượng nghiệp vụ, chứa cả logic|
|**Phụ thuộc**|Phụ thuộc vào ORM như Entity Framework, Dapper|Không phụ thuộc vào ORM, CSDL hay framework|
|**Logic nghiệp vụ**|Không chứa hoặc rất ít logic|Chứa đầy đủ logic nghiệp vụ liên quan|
|**Ví dụ**|`DbSet<Product>` trong Entity Framework|`Product` có phương thức kiểm tra, tính toán giá, thay đổi trạng thái...|

---
## Examples
``` c#
public class Product
{
    public Guid Id { get; private set; }  // Định danh duy nhất
    public string Name { get; private set; }
    public decimal Price { get; private set; }
    public int Stock { get; private set; }  

    public Product(string name, decimal price, int stock)
    {
        if (string.IsNullOrWhiteSpace(name))
            throw new ArgumentException("Tên sản phẩm không được để trống.");
        if (price <= 0)
            throw new ArgumentException("Giá phải lớn hơn 0.");
        if (stock < 0)
            throw new ArgumentException("Số lượng tồn kho không thể âm.");
        Id = Guid.NewGuid();
        Name = name;
        Price = price;
        Stock = stock;
    }

    public void UpdatePrice(decimal newPrice)
    {
        if (newPrice <= 0)
            throw new ArgumentException("Giá mới phải lớn hơn 0.");
        Price = newPrice;
    }

    public void ReduceStock(int quantity)
    {
        if (quantity <= 0)
            throw new ArgumentException("Số lượng giảm phải lớn hơn 0.");
        if (quantity > Stock)
            throw new InvalidOperationException("Không đủ hàng trong kho.");
        Stock -= quantity;
    }
}
```

### **Điểm đặc biệt của Entity trong Clean Architecture**
1. **Không phụ thuộc vào CSDL**
    - Không có thuộc tính `[Key]` hay `DbSet<Product>` vì nó không cần biết dữ liệu sẽ được lưu ở đâu.
    - CSDL chỉ là một cách để lưu trữ entity này, không phải phần cốt lõi của nó.
    
2. **Chứa logic nghiệp vụ**
    - Có kiểm tra đầu vào khi tạo sản phẩm (`if (price <= 0) throw new ArgumentException(...)`).
    - Có logic kiểm tra khi cập nhật giá (`UpdatePrice` phải đảm bảo giá mới hợp lệ).
    - Có logic trừ hàng trong kho (`ReduceStock` kiểm tra số lượng tồn kho trước khi trừ).

