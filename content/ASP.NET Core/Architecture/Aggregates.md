---
title: Aggregates
tags:
  - architectures
  - Full-Stack
---

- **Định nghĩa**: **Aggregate** là một tập hợp các **[[ASP.NET Core/Architecture/Entity|Entity]]** và **[[Value Object]]** có quan hệ chặt chẽ, được nhóm lại để đảm bảo **tính nhất quán** và **toàn vẹn** của dữ liệu. Mỗi Aggregate có một **Aggregate Root**, là điểm truy cập duy nhất để tương tác với các thành phần bên trong.
    
- **Mục đích**:
    - Đảm bảo rằng mọi thao tác trên các thành phần bên trong Aggregate đều phải thông qua Aggregate Root, giúp duy trì **tính toàn vẹn** của dữ liệu.
    - Giảm thiểu sự phụ thuộc và tương tác trực tiếp giữa các Aggregate, tăng cường **tính đóng gói** và **bảo trì** của hệ thống.


### Ví dụ
##### 1. Entity: OrderItem
``` c#
public class OrderItem
{
    public Guid Id { get; private set; }
    public Guid ProductId { get; private set; }
    public int Quantity { get; private set; }
    public decimal UnitPrice { get; private set; }

    public OrderItem(Guid productId, int quantity, decimal unitPrice)
    {
        if (quantity <= 0)
            throw new ArgumentException("Số lượng phải lớn hơn 0.");
        if (unitPrice <= 0)
            throw new ArgumentException("Đơn giá phải lớn hơn 0.");

        Id = Guid.NewGuid();
        ProductId = productId;
        Quantity = quantity;
        UnitPrice = unitPrice;
    }

    public decimal GetTotalPrice()
    {
        return Quantity * UnitPrice;
    }
}
```

##### 2. Aggregate Root: Order
``` c#
public class Order
{
    public Guid Id { get; private set; }
    public DateTime OrderDate { get; private set; }
    private List<OrderItem> _orderItems = new List<OrderItem>();
    public IReadOnlyCollection<OrderItem> OrderItems => _orderItems.AsReadOnly();

    public Order()
    {
        Id = Guid.NewGuid();
        OrderDate = DateTime.UtcNow;
    }

    public void AddOrderItem(Guid productId, int quantity, decimal unitPrice)
    {
        var existingItem = _orderItems.FirstOrDefault(item => item.ProductId == productId);
        if (existingItem != null)
        {
            // Nếu sản phẩm đã tồn tại trong đơn hàng, tăng số lượng
            existingItem.IncreaseQuantity(quantity);
        }
        else
        {
            // Nếu sản phẩm chưa có trong đơn hàng, thêm mới
            var orderItem = new OrderItem(productId, quantity, unitPrice);
            _orderItems.Add(orderItem);
        }
    }

    public void RemoveOrderItem(Guid orderItemId)
    {
        var orderItem = _orderItems.FirstOrDefault(item => item.Id == orderItemId);
        if (orderItem != null)
        {
            _orderItems.Remove(orderItem);
        }
        else
        {
            throw new ArgumentException("Không tìm thấy mục đơn hàng.");
        }
    }

    public decimal GetTotalOrderPrice()
    {
        return _orderItems.Sum(item => item.GetTotalPrice());
    }
}

```