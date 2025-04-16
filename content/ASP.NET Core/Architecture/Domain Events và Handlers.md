---
title: Domain Events và Handlers
tags:
  - architectures
  - Full-Stack
---
# **Sự kiện miền (Domain Events) và Bộ xử lý (Handlers) trong Clean Architecture**

## **1. Định nghĩa**
- **Domain Event** là một sự kiện xảy ra trong hệ thống và có ý nghĩa đối với nghiệp vụ.
- **Event Handler** là thành phần xử lý sự kiện khi nó được kích hoạt.
- Mục đích chính là **giảm sự phụ thuộc trực tiếp giữa các phần của ứng dụng** và hỗ trợ **kiến trúc hướng sự kiện (event-driven architecture)**.

### **Ví dụ thực tế:**
Khi một **đơn hàng được tạo**, hệ thống có thể cần:
✅ Gửi email xác nhận cho khách hàng.
✅ Cập nhật số lượng hàng tồn kho.
✅ Ghi log sự kiện.

Thay vì viết tất cả logic này trong `OrderService`, ta có thể **phát một Sự kiện miền (Domain Event)**, và mỗi tác vụ sẽ có một **Bộ xử lý sự kiện (Event Handler)** riêng để xử lý.

---

## **2. Khi nào nên sử dụng Sự kiện miền?**
✔ Khi một hành động kéo theo nhiều nghiệp vụ khác nhau.
✔ Khi muốn **giảm sự phụ thuộc giữa các dịch vụ**, giúp code dễ bảo trì hơn.
✔ Khi xử lý **tác vụ bất đồng bộ (async)** như gửi email, ghi log, cập nhật dữ liệu.

🚫 Không nên sử dụng nếu chỉ có **một hành động duy nhất** mà không kéo theo các tác vụ khác.

---

## **3. Ví dụ về Sự kiện miền và Bộ xử lý trong hệ thống Đơn hàng**

### **3.1. Định nghĩa Interface `IDomainEvent`**
```csharp
public interface IDomainEvent
{
    DateTime OccurredOn { get; }
}
```

---

### **3.2. Tạo Sự kiện miền: `OrderCreatedEvent`**
```csharp
public class OrderCreatedEvent : IDomainEvent
{
    public Guid OrderId { get; }
    public Guid CustomerId { get; }
    public DateTime OccurredOn { get; } = DateTime.UtcNow;

    public OrderCreatedEvent(Guid orderId, Guid customerId)
    {
        OrderId = orderId;
        CustomerId = customerId;
    }
}
```

---

### **3.3. Phát sự kiện khi tạo đơn hàng**
```csharp
public class OrderService
{
    private readonly IOrderRepository _orderRepository;
    private readonly IDomainEventDispatcher _eventDispatcher;

    public OrderService(IOrderRepository orderRepository, IDomainEventDispatcher eventDispatcher)
    {
        _orderRepository = orderRepository;
        _eventDispatcher = eventDispatcher;
    }

    public async Task<Order> CreateOrderAsync(Guid customerId, List<OrderItem> orderItems)
    {
        var order = new Order(customerId, orderItems);
        await _orderRepository.AddAsync(order);

        var orderCreatedEvent = new OrderCreatedEvent(order.Id, customerId);
        await _eventDispatcher.DispatchAsync(orderCreatedEvent);

        return order;
    }
}
```

---

### **3.4. Tạo Bộ xử lý sự kiện**

#### **Handler 1: Gửi email xác nhận đơn hàng**
```csharp
public class SendOrderConfirmationEmailHandler : IDomainEventHandler<OrderCreatedEvent>
{
    private readonly IEmailService _emailService;

    public SendOrderConfirmationEmailHandler(IEmailService emailService)
    {
        _emailService = emailService;
    }

    public async Task HandleAsync(OrderCreatedEvent domainEvent)
    {
        var subject = "Xác nhận đơn hàng: " + domainEvent.OrderId;
        var body = $"Đơn hàng của bạn đã được tạo thành công vào {domainEvent.OccurredOn}.";
        await _emailService.SendEmailAsync(domainEvent.CustomerId, subject, body);
    }
}
```

#### **Handler 2: Cập nhật tồn kho sản phẩm**
```csharp
public class UpdateProductStockHandler : IDomainEventHandler<OrderCreatedEvent>
{
    private readonly IProductRepository _productRepository;

    public UpdateProductStockHandler(IProductRepository productRepository)
    {
        _productRepository = productRepository;
    }

    public async Task HandleAsync(OrderCreatedEvent domainEvent)
    {
        var order = await _orderRepository.GetByIdAsync(domainEvent.OrderId);
        foreach (var item in order.OrderItems)
        {
            var product = await _productRepository.GetByIdAsync(item.ProductId);
            product.ReduceStock(item.Quantity);
            await _productRepository.UpdateAsync(product);
        }
    }
}
```

---

### **3.5. Cơ chế Dispatcher để phát sự kiện**
```csharp
public interface IDomainEventDispatcher
{
    Task DispatchAsync<T>(T domainEvent) where T : IDomainEvent;
}
```

🚀 **Triển khai Dispatcher sử dụng Mediator Pattern:**
```csharp
public class DomainEventDispatcher : IDomainEventDispatcher
{
    private readonly IServiceProvider _serviceProvider;

    public DomainEventDispatcher(IServiceProvider serviceProvider)
    {
        _serviceProvider = serviceProvider;
    }

    public async Task DispatchAsync<T>(T domainEvent) where T : IDomainEvent
    {
        var handlers = _serviceProvider.GetServices<IDomainEventHandler<T>>();

        foreach (var handler in handlers)
        {
            await handler.HandleAsync(domainEvent);
        }
    }
}
```

---

## **4. Tại sao sử dụng Sự kiện miền?**
✔ **Tách biệt logic nghiệp vụ** – `OrderService` không cần biết chuyện gì xảy ra sau khi đơn hàng được tạo.
✔ **Dễ bảo trì** – Khi cần thêm chức năng mới, chỉ cần tạo một Handler mới.
✔ **Hỗ trợ xử lý bất đồng bộ (async)** – Gửi email, cập nhật tồn kho có thể chạy song song.
✔ **Tăng khả năng mở rộng** – Dễ dàng thêm Handler mới mà không cần sửa code cũ.

🚀 **Ví dụ: Cần gửi tin nhắn SMS khi tạo đơn hàng?**
→ Chỉ cần thêm một `OrderCreatedSmsHandler` mà không cần sửa `OrderService`!

---

## **5. Kết luận**

| **Đặc điểm**           | **Sự kiện miền & Bộ xử lý** |
|-----------------------|--------------------------|
| **Tách biệt logic nghiệp vụ** | ✅ Có |
| **Hỗ trợ xử lý bất đồng bộ** | ✅ Có |
| **Hỗ trợ mở rộng dễ dàng** | ✅ Có |
| **Phát sự kiện khi có thay đổi quan trọng** | ✅ Có |
| **Không làm phức tạp hóa nghiệp vụ đơn giản** | ❌ Không |

💡 **Sự kiện miền giúp xây dựng hệ thống linh hoạt, dễ mở rộng và tách biệt trách nhiệm rõ ràng! 🚀**
