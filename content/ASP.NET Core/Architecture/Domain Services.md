---
title: Domain Services
tags:
  - architectures
  - Full-Stack
---
### **Domain Services trong Clean Architecture là gì?**

#### **1. Định nghĩa**

- **Domain Services** là các lớp chứa **logic nghiệp vụ không thuộc về một Entity cụ thể** hoặc liên quan đến nhiều **Entity**.
- Được sử dụng khi một hành động **cần phối hợp nhiều Entity để hoàn thành** nhưng không nên đặt logic đó vào bất kỳ Entity nào.
- **Không lưu trạng thái (stateless)** – Domain Services chỉ thực hiện hành vi, không chứa trạng thái riêng.

---

#### **2. Khi nào cần dùng Domain Services?**

- Khi một logic nghiệp vụ **liên quan đến nhiều Entity** và không thuộc về riêng một Entity nào.
- Khi cần thực hiện **tính toán phức tạp**, **quy tắc nghiệp vụ**, hoặc **giao tiếp giữa các Aggregate**.
- Khi muốn giữ **Entity đơn giản**, chỉ chứa những gì thực sự thuộc về nó.

💡 **Nguyên tắc quan trọng:**

- **Không chứa trạng thái** – Không lưu dữ liệu bên trong, chỉ xử lý logic.
- **Không thay thế Entity** – Chỉ dùng khi logic không thể đặt trong Entity.
- **Chỉ thao tác trên Entity, Value Object hoặc các dữ liệu liên quan đến Domain** – Không chứa code liên quan đến UI, Database, hoặc Infrastructure.

---

### **3. Ví dụ về Domain Services trong hệ thống Order**

#### **Tình huống:**

Chúng ta có hệ thống **Order** với các **Product**. Khi khách hàng đặt hàng, chúng ta cần:

- Kiểm tra xem **tồn kho có đủ không**.
- Nếu đủ hàng, trừ số lượng hàng trong kho và tạo Order.
- Nếu không đủ hàng, trả về lỗi.

#### **Cách tiếp cận sai: Đặt logic này trong Entity**

- Nếu đặt trong `Order`, thì Order phải biết về tồn kho của sản phẩm → **vi phạm nguyên tắc tách biệt trách nhiệm (SRP - Single Responsibility Principle)**.
- Nếu đặt trong `Product`, thì Product sẽ biết về đơn hàng → **không hợp lý** vì một sản phẩm có thể thuộc nhiều đơn hàng khác nhau.

💡 **Giải pháp đúng: Sử dụng Domain Service**

#### **3.1. Interface của Product Repository**

Vì **Domain Service không làm việc với cơ sở dữ liệu**, nó sẽ gọi đến Repository để lấy dữ liệu.
``` csharp
public interface IProductRepository
{
    Task<Product> GetByIdAsync(Guid productId);
    Task UpdateAsync(Product product);
}
```
#### **3.2. Domain Service: `OrderService`**

Chứa **logic tạo đơn hàng** mà không đặt nó vào `Order` hoặc `Product`.
``` csharp
public class OrderService
{
    private readonly IProductRepository _productRepository;

    public OrderService(IProductRepository productRepository)
    {
        _productRepository = productRepository;
    }

    public async Task<Order> CreateOrderAsync(Guid customerId, List<(Guid ProductId, int Quantity)> orderItems)
    {
        var order = new Order(customerId);

        foreach (var item in orderItems)
        {
            var product = await _productRepository.GetByIdAsync(item.ProductId);
            if (product == null)
                throw new Exception($"Sản phẩm {item.ProductId} không tồn tại.");

            if (product.Stock < item.Quantity)
                throw new Exception($"Sản phẩm {product.Name} không đủ hàng trong kho.");

            product.ReduceStock(item.Quantity); // Trừ hàng trong kho
            order.AddOrderItem(product.Id, item.Quantity, product.Price);
        }

        // Cập nhật số lượng tồn kho sau khi đặt hàng thành công
        foreach (var item in orderItems)
        {
            var product = await _productRepository.GetByIdAsync(item.ProductId);
            await _productRepository.UpdateAsync(product);
        }

        return order;
    }
}
```

---

### **4. Giải thích chi tiết**

📌 **Tại sao không đặt logic này trong Entity?**

- `Product` chỉ nên biết về thông tin của chính nó (tên, giá, tồn kho), không nên biết về Order.
- `Order` chỉ nên biết danh sách sản phẩm mà nó chứa, không nên trực tiếp kiểm tra kho hàng.
- **Domain Service giúp tách biệt logic liên quan đến nhiều Entity, giữ cho mỗi Entity có trách nhiệm riêng.**

📌 **Tại sao không dùng Application Service thay vì Domain Service?**

- **Application Service (Service Layer)** thường xử lý luồng nghiệp vụ chung, gọi đến nhiều Domain Services và thực hiện các thao tác liên quan đến Infrastructure.
- **Domain Service chỉ tập trung vào logic nghiệp vụ thuần túy**, không chứa mã liên quan đến UI, database, logging...

---

### **5. Khi nào KHÔNG nên dùng Domain Service?**

🚫 **Không sử dụng nếu logic chỉ liên quan đến một Entity** → Đặt logic vào Entity thay vì Domain Service.  
🚫 **Không sử dụng nếu chỉ để lấy dữ liệu từ database** → Đó là nhiệm vụ của Repository.  
🚫 **Không sử dụng nếu chỉ xử lý luồng tổng quát của ứng dụng** → Đó là nhiệm vụ của Application Service.

---

### **6. Tóm lại**

|**Đặc điểm**|**Domain Service**|
|---|---|
|**Chứa logic nghiệp vụ**|✅ Có|
|**Làm việc với nhiều Entity**|✅ Có|
|**Có trạng thái riêng**|❌ Không|
|**Giao tiếp với Repository**|✅ Có|
|**Truy vấn dữ liệu**|❌ Không (Repository làm việc này)|
|**Thực hiện nghiệp vụ hệ thống (Workflow)**|❌ Không (Application Service làm việc này)|

💡 **Domain Service giúp giữ cho Entity gọn gàng, tách biệt rõ ràng logic nghiệp vụ phức tạp và làm cho ứng dụng dễ bảo trì hơn.** 🚀