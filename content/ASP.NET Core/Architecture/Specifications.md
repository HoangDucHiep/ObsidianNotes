---
title: Specifications
tags:
  - Full-Stack
  - architectures
---
### **Specifications trong Clean Architecture là gì?**

#### **1. Định nghĩa**
**Specification Pattern** là một mẫu thiết kế giúp tách biệt **logic truy vấn dữ liệu** ra khỏi **Repository**, giúp viết các tiêu chí lọc dữ liệu một cách **tái sử dụng** và **dễ bảo trì** hơn.

💡 **Tại sao cần Specification?**
- Nếu đặt logic truy vấn trực tiếp vào **Repository**, khi yêu cầu thay đổi hoặc mở rộng, chúng ta phải chỉnh sửa nhiều nơi.
- Specification giúp viết tiêu chí lọc dữ liệu dưới dạng **đối tượng có thể tái sử dụng**.
- Dễ kết hợp nhiều tiêu chí lọc khác nhau mà không cần viết lại toàn bộ truy vấn.

---

#### **2. Khi nào cần dùng Specification?**

✔ Khi có nhiều tiêu chí lọc khác nhau cho cùng một Entity.  
✔ Khi muốn **kết hợp nhiều điều kiện tìm kiếm một cách linh hoạt** mà không cần viết lại nhiều lần.  
✔ Khi muốn **định nghĩa logic nghiệp vụ liên quan đến dữ liệu truy vấn** một cách rõ ràng, tách biệt khỏi Repository.

---

### **3. Ví dụ về Specification trong hệ thống Order**

#### **Tình huống**

Giả sử chúng ta có hệ thống Order, chúng ta muốn tìm các đơn hàng theo nhiều tiêu chí:

- Tìm **đơn hàng theo trạng thái**.
- Tìm **đơn hàng theo khoảng ngày đặt hàng**.
- Tìm **đơn hàng theo khách hàng**.
- Kết hợp nhiều tiêu chí lại với nhau.

💡 **Sử dụng Specification giúp chúng ta dễ dàng xây dựng và kết hợp các tiêu chí tìm kiếm này!**

---

### **4. Cài đặt Specification Pattern**

#### **4.1. Interface chung cho Specification**

Chúng ta cần một interface chung để định nghĩa tiêu chí lọc.
``` csharp
using System;
using System.Linq.Expressions;

public interface ISpecification<T>
{
    Expression<Func<T, bool>> Criteria { get; }
}
```

🚀 **Giải thích**:  
✅ `Criteria` là một **biểu thức lambda** dùng để lọc dữ liệu (ví dụ: `o => o.Status == "Shipped"`).  
✅ `T` là kiểu Entity mà Specification áp dụng (ví dụ: `Order`).

---

#### **4.2. Các Specification cụ thể**

💡 **Tạo Specification để tìm đơn hàng theo trạng thái:**
``` csharp
public class OrderByStatusSpecification : ISpecification<Order>
{
    public string Status { get; }

    public OrderByStatusSpecification(string status)
    {
        Status = status;
    }

    public Expression<Func<Order, bool>> Criteria =>
        order => order.Status == Status;
}
```

💡 **Tạo Specification để tìm đơn hàng trong khoảng ngày:**
``` csharp
public class OrderByDateRangeSpecification : ISpecification<Order>
{
    public DateTime StartDate { get; }
    public DateTime EndDate { get; }

    public OrderByDateRangeSpecification(DateTime startDate, DateTime endDate)
    {
        StartDate = startDate;
        EndDate = endDate;
    }

    public Expression<Func<Order, bool>> Criteria =>
        order => order.OrderDate >= StartDate && order.OrderDate <= EndDate;
}
```

💡 **Tạo Specification để tìm đơn hàng theo khách hàng:**
``` csharp
public class OrderByCustomerSpecification : ISpecification<Order>
{
    public Guid CustomerId { get; }

    public OrderByCustomerSpecification(Guid customerId)
    {
        CustomerId = customerId;
    }

    public Expression<Func<Order, bool>> Criteria =>
        order => order.CustomerId == CustomerId;
}
```

---

#### **4.3. Áp dụng Specification trong Repository**

Chúng ta cập nhật `IOrderRepository` để hỗ trợ Specification.
``` csharp
public interface IOrderRepository
{
    Task<IEnumerable<Order>> GetOrdersBySpecificationAsync(ISpecification<Order> specification);
}
```

Cài đặt trong **OrderRepository**:↳
``` csharp
public class OrderRepository : IOrderRepository
{
    private readonly ApplicationDbContext _context;

    public OrderRepository(ApplicationDbContext context)
    {
        _context = context;
    }

    public async Task<IEnumerable<Order>> GetOrdersBySpecificationAsync(ISpecification<Order> specification)
    {
        return await _context.Orders
            .Where(specification.Criteria)
            .ToListAsync();
    }
}
```

🚀 **Giải thích**:  
✅ `Where(specification.Criteria)` giúp lọc đơn hàng theo điều kiện của Specification.  
✅ Không cần viết nhiều phương thức khác nhau trong Repository.

---

### **5. Sử dụng Specification trong Service**

Bây giờ, ta có thể sử dụng Specification một cách dễ dàng trong Service.

Ví dụ: Tìm tất cả đơn hàng **đang giao hàng** trong tháng này.
``` csharp
var spec = new OrderByStatusSpecification("Shipped");
var orders = await _orderRepository.GetOrdersBySpecificationAsync(spec);
```

Ví dụ: Tìm tất cả đơn hàng của một khách hàng trong khoảng thời gian.
``` csharp
var spec = new OrderByCustomerSpecification(customerId);
var dateSpec = new OrderByDateRangeSpecification(DateTime.UtcNow.AddDays(-30), DateTime.UtcNow);

var customerOrders = await _orderRepository.GetOrdersBySpecificationAsync(spec);
var recentOrders = await _orderRepository.GetOrdersBySpecificationAsync(dateSpec);
```

---

### **6. Khi nào KHÔNG nên dùng Specification?**

🚫 Khi chỉ có **một hoặc hai tiêu chí lọc đơn giản**, có thể đặt trực tiếp vào Repository.  
🚫 Khi không cần **tái sử dụng** tiêu chí lọc ở nhiều nơi khác nhau.  
🚫 Khi tiêu chí tìm kiếm quá phức tạp, có thể cần một Query Object hoặc dịch vụ tìm kiếm chuyên biệt.

---

### **7. Kết luận**

| **Đặc điểm**                                               | **Specification Pattern** |
| ---------------------------------------------------------- | ------------------------- |
| **Tách biệt logic truy vấn khỏi Repository**               | ✅ Có                      |
| **Có thể tái sử dụng nhiều lần**                           | ✅ Có                      |
| **Kết hợp nhiều tiêu chí linh hoạt**                       | ✅ Có                      |
| **Tránh viết nhiều phương thức tìm kiếm trong Repository** | ✅ Có                      |
| **Làm đơn giản code trong Service**                        | ✅ Có                      |

💡 **Lợi ích của Specification**:  
✅ **Dễ bảo trì** – Khi cần thay đổi tiêu chí lọc, chỉ sửa trong Specification.  
✅ **Tái sử dụng cao** – Dùng lại tiêu chí lọc ở nhiều nơi mà không cần viết lại truy vấn.  
✅ **Linh hoạt** – Dễ dàng kết hợp nhiều tiêu chí lọc mà không làm phình to Repository.