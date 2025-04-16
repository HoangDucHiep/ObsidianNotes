# **Tổng hợp các khái niệm và ví dụ trong Clean Architecture với ASP.NET Core**

## **1️⃣ Monolithic Applications và Containers**
- **Monolithic Application**: Ứng dụng nguyên khối, được triển khai dưới dạng **một container duy nhất**.
- **Nhược điểm**: Khi ứng dụng phát triển, cần **scale toàn bộ ứng dụng**, không thể scale từng thành phần riêng lẻ.
- **Triển khai với Docker**: Sử dụng Docker để containerize ứng dụng giúp triển khai nhanh hơn.
- **Tích hợp với Azure**: Có thể deploy lên Azure App Services hoặc Azure Virtual Machine Scale Sets.

---

## **2️⃣ Entity Framework Core (EF Core)**
- **ORM** giúp ánh xạ giữa Object trong C# và bảng trong database.
- **Hỗ trợ nhiều loại database**: SQL Server, PostgreSQL, MySQL, SQLite...
- **Cài đặt**:
  ```sh
  dotnet add package Microsoft.EntityFrameworkCore
  dotnet add package Microsoft.EntityFrameworkCore.SqlServer
  ```
- **Tạo DbContext**:
  ```csharp
  public class ApplicationDbContext : DbContext
  {
      public DbSet<Product> Products { get; set; }
      public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) {}
  }
  ```
- **Migration & Database Update**:
  ```sh
  dotnet ef migrations add InitialCreate
  dotnet ef database update
  ```

---

## **3️⃣ Repository Pattern & Unit of Work**
- **Repository** giúp **tách biệt logic truy vấn dữ liệu khỏi Service**.
- **Unit of Work** giúp **quản lý transaction** khi dùng nhiều repository cùng lúc.
- **Ví dụ về Unit of Work**:
  ```csharp
  public class UnitOfWork : IUnitOfWork
  {
      private readonly ApplicationDbContext _context;
      private IDbContextTransaction _transaction;

      public async Task BeginTransactionAsync() => _transaction = await _context.Database.BeginTransactionAsync();
      public async Task CommitTransactionAsync() { await _context.SaveChangesAsync(); await _transaction.CommitAsync(); }
      public async Task RollbackTransactionAsync() => await _transaction.RollbackAsync();
  }
  ```

---

## **4️⃣ MediatR trong ASP.NET Core**
- **Mediator Pattern** giúp **tách biệt Controller và Business Logic**.
- **Cài đặt MediatR**:
  ```sh
  dotnet add package MediatR.Extensions.Microsoft.DependencyInjection
  ```
- **Ví dụ Query với MediatR**:
  ```csharp
  public record GetOrderByIdQuery(Guid OrderId) : IRequest<OrderDto>;

  public class GetOrderByIdHandler : IRequestHandler<GetOrderByIdQuery, OrderDto>
  {
      private readonly IOrderRepository _orderRepository;
      public async Task<OrderDto> Handle(GetOrderByIdQuery request, CancellationToken cancellationToken)
      {
          var order = await _orderRepository.GetByIdAsync(request.OrderId);
          return order == null ? null : new OrderDto(order.Id, order.CustomerName, order.TotalPrice);
      }
  }
  ```
- **Gọi từ Controller**:
  ```csharp
  [HttpGet("{id}")]
  public async Task<IActionResult> GetOrderById(Guid id)
  {
      var order = await _mediator.Send(new GetOrderByIdQuery(id));
      return order == null ? NotFound() : Ok(order);
  }
  ```

---

## **5️⃣ Custom Exceptions & Guard Clauses**
- **Custom Exception giúp định nghĩa lỗi rõ ràng**:
  ```csharp
  public class ProductNotFoundException : Exception
  {
      public ProductNotFoundException(Guid productId) : base($"Sản phẩm {productId} không tồn tại.") {}
  }
  ```
- **Guard Clauses giúp kiểm tra dữ liệu đầu vào nhanh chóng**:
  ```csharp
  public static class Guard
  {
      public static void AgainstNull(object value, string parameterName)
      {
          if (value == null)
              throw new ArgumentNullException(parameterName, $"{parameterName} không thể null.");
      }
  }
  ```

---

## **6️⃣ Clean Architecture: Phân chia tầng**
```
├── Application (Business Logic)
│   ├── Interfaces
│   ├── Services
│   ├── DTOs
│   ├── Exceptions
│   ├── GuardClauses
├── Domain (Entities, Aggregates, Value Objects, Domain Events)
│   ├── Entities
│   ├── Aggregates
│   ├── ValueObjects
│   ├── Events
├── Infrastructure (Database, External Services)
│   ├── Persistence (Repositories, DbContext)
│   ├── Services (Email, SMS, Logging)
│   ├── EventDispatcher
├── Presentation (API Controllers, Middleware)
│   ├── Controllers
│   ├── Middlewares
├── WebAPI (Startup, Configurations)
├── Frontend (React, Vue)
```

---

## **7️⃣ Tích hợp React vào ASP.NET Core**
### **Cách 1: React tách biệt với Backend**
```
├── frontend (React App)
│   ├── src
│   ├── public
│   ├── package.json
├── backend (ASP.NET Core API)
│   ├── src
│   ├── WebAPI
│   ├── appsettings.json
```
**Triển khai Backend:**
```sh
cd backend
 dotnet build
 dotnet run
```
**Triển khai Frontend:**
```sh
cd frontend
npm install
npm run build
```

### **Cách 2: Đặt React trong ASP.NET Core**
- **Cấu hình `Startup.cs` để chạy React**:
  ```csharp
  public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
  {
      app.UseSpa(spa =>
      {
          spa.Options.SourcePath = "ClientApp";
          if (env.IsDevelopment())
              spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
      });
  }
  ```
- **Chạy React kèm theo Backend:**
  ```sh
  dotnet run
  cd ClientApp && npm start
  ```

---

### **📌 Tổng kết**
✅ **Monolithic Application có thể containerize để scale dễ hơn**.  
✅ **EF Core giúp làm việc với database dễ dàng hơn**.  
✅ **Repository Pattern + Unit of Work giúp kiểm soát transaction tốt hơn**.  
✅ **MediatR giúp tách biệt Controller với Business Logic**.  
✅ **Clean Architecture phân chia rõ các tầng Domain, Application, Infrastructure, Presentation**.  
✅ **React có thể tích hợp vào ASP.NET Core hoặc deploy riêng**.  

🔥 **Kiến trúc Clean giúp ứng dụng dễ bảo trì, mở rộng và kiểm thử! 🚀**
