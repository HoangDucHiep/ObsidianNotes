---
title: Common web application architectures
tags:
  - Full-Stack
  - architectures
  - "#NET"
node_size: "2"
---
### Monolithic application (nguyên khối)
- Một ứng dụng nguyên khối là một ứng dụng hoàn toàn độc lập về mặt hành vi. Nó có thể tương tác với các dịch vụ hoặc kho dữ liệu khác trong quá trình thực hiện các hoạt động của mình, nhưng phần cốt lõi của hành vi ứng dụng chạy trong một quy trình riêng và toàn bộ ứng dụng thường được triển khai như một đơn vị duy nhất. 
- Nếu ứng dụng cần mở rộng theo chiều ngang, thường toàn bộ ứng dụng sẽ được nhân bản trên nhiều máy chủ hoặc máy ảo khác nhau.

### All-in-one applications
- Trong kiến trúc này, toàn bộ logic của ứng dụng được chứa trong một dự án duy nhất, biên dịch thành một tệp thực thi (assembly) duy nhất và triển khai dưới dạng một đơn vị duy nhất.
![[Pasted image 20250225135937.png]]
- Project ASP.net core MVC như trên, đạt được separation of concerns bằng các folder
- - **Cấu trúc thư mục**:
    - **Views**: Giao diện trình bày
    - **Data**: Truy cập dữ liệu
    - **Models/Services**: Logic nghiệp vụ
- **Nhược điểm**: Khi dự án lớn, dễ phát sinh **spaghetti code**, khó quản lý UI và logic bị phân tán.
- **Giải pháp**: Chuyển sang **kiến trúc đa dự án** để tách biệt các lớp (UI, Business, Data).
### **Lớp (Layers) là gì?**
- Khi ứng dụng trở nên phức tạp, một cách để quản lý là **chia ứng dụng theo từng trách nhiệm hoặc mối quan tâm (concerns)**. Cách tiếp cận này tuân theo nguyên tắc **tách biệt các mối quan tâm (Separation of Concerns)**, giúp tổ chức mã nguồn tốt hơn và giúp lập trình viên dễ dàng tìm thấy nơi triển khai các chức năng cụ thể.
##### **Lợi ích của kiến trúc phân lớp:**
- **Tái sử dụng mã nguồn**: Các chức năng chung có thể được tái sử dụng trên toàn bộ ứng dụng, tuân theo nguyên tắc **Don't Repeat Yourself (DRY)**.
- **Đảm bảo tính đóng gói (Encapsulation)**:
    - Kiểm soát lớp nào có thể giao tiếp với lớp nào.
    - Khi thay đổi một lớp, chỉ các lớp liên quan bị ảnh hưởng, giảm tác động lan truyền.
- **Dễ dàng thay thế hoặc mở rộng**:
    - Ví dụ: Nếu ban đầu ứng dụng sử dụng SQL Server, có thể dễ dàng thay đổi sang một giải pháp lưu trữ trên đám mây mà không ảnh hưởng đến toàn bộ ứng dụng.
- **Dễ dàng kiểm thử (Testing)**:
    - Có thể thay thế các lớp thực bằng các phiên bản giả lập (mock) để kiểm thử nhanh hơn và hiệu quả hơn.

## **N-Layer architecture applications**
![[Pasted image 20250225153108.png]]
- Cách tầng được viết tắt là ***UI, BLL (Business Logic Layer), and DAL (Data Access Layer)***.
- Với kiến trúc này, người dùng tạo các request thông qua tâng UI, sau đó tầng UI tương tác với duy nhất BLL, và BLL lại tương tác với DAL khi cần access data.![[Pasted image 20250225154048.png]]

## **Clean architecture**
- ***Clean architecture*** đặt **business logic** và **application model** vào **trung tâm của ứng dụng**.
- Thay vì để **business logic** phụ thuộc vào **data access** hoặc các **infrastructure** khác, **sự phụ thuộc này được đảo ngược**: **hạ tầng và các chi tiết triển khai sẽ phụ thuộc vào Application Core**.
- Cách tiếp cận này được thực hiện bằng cách **định nghĩa các abstraction (hoặc interfaces) trong Application Core**, sau đó các lớp trong **Infrastructure** sẽ triển khai chúng.![[Pasted image 20250225155240.png]]![[Pasted image 20250225155938.png]]
	- ***Application Core***, không phụ thuộc vào bất cứ phần nào khác
	- ***Application's entities and interfaces*** ở trong cùng
	- ***Domain services***, vẫn thuộc application core, nơi implement các interfaces được định nghĩa bên trong cùng
	- ***Infrastructure***, là nơi chứa data access, các services (như logging, email service, ...), External Integrations, configuration, DI, ...
![[Pasted image 20250225160348.png]]
## Organizing code in Clean Architecture
##### Application Core
- Tầng **Application Core** giữ **mô hình nghiệp vụ (Business Model)**, bao gồm **entities, services, và interfaces**. Các **interfaces** trong tầng này là **abstraction** (trừu tượng hóa) cho các thao tác sẽ được triển khai trong **Infrastructure** (truy cập dữ liệu, hệ thống tệp, gọi API...).
- Đôi khi, các dịch vụ hoặc interface trong tầng này cần làm việc với **các kiểu dữ liệu không phải entity** và không phụ thuộc vào **UI hoặc Infrastructure**. Những kiểu này thường được định nghĩa dưới dạng **[Data Transfer Objects (DTOs)](https://learn.microsoft.com/vi-vn/aspnet/web-api/overview/data/using-web-api-with-entity-framework/part-5)**.
##### Thành phần chính trong Application Core:
1. **[[Entities]]** – Các lớp mô hình nghiệp vụ được lưu trữ trong cơ sở dữ liệu.
2. **[[Aggregates]]** – Nhóm các **Entities** có liên kết chặt chẽ, tuân theo **Domain-Driven Design (DDD)**.
3. **Interfaces** – Định nghĩa các giao diện cho **Repositories, Services, và Infrastructure**.
4. **[[Domain Services]]** – Chứa logic nghiệp vụ phức tạp không thuộc về một entity cụ thể.
5. **[[Specifications]]** – Định nghĩa các tiêu chí truy vấn dữ liệu theo mô hình **Specification Pattern**.
6. **[[Custom Exceptions và Guard Clauses]]** – Xử lý lỗi nghiệp vụ và kiểm tra dữ liệu đầu vào.
7. **[[Domain Events và Handlers]]** – Hỗ trợ **event-driven architecture**, giúp các phần của ứng dụng giao tiếp với nhau mà không cần phụ thuộc chặt chẽ.

## Infrastructure
- ***Infrastructure project*** thường bao gồm data access implementations.
- Trong một ứng dụng web ASP.NET Core điển hình, các triển khai này bao gồm DBContext Framework (EF), bất kỳ đối tượng di chuyển lõi EF nào đã được xác định và các lớp triển khai truy cập dữ liệu. 
- Cách phổ biến nhất để trừu tượng mã truy cập truy cập dữ liệu là thông qua việc sử dụng [Repository Patterns](https://deviq.com/design-patterns/repository-pattern)
##### Infrastructure types
- EF Core types (`DbContext`, `Migration`)
- Data access implementation types (Repositories)
- Infrastructure-specific services (for example, `FileLogger` or `SmtpNotifier`)
## UI Layer
- Lớp giao diện người dùng trong ứng dụng MVC ASP.NET Core là điểm nhập cho ứng dụng. Dự án này nên tham chiếu dự án lõi ứng dụng và các loại của nó nên tương tác với cơ sở hạ tầng hoàn toàn thông qua các giao diện được xác định trong lõi ứng dụng. Không nên khởi tạo trực tiếp hoặc các cuộc gọi tĩnh đến các loại lớp cơ sở hạ tầng trong lớp UI.
##### UI Layer types
- Controllers
- Custom Filters
- Custom Middleware
- Views
- ViewModels
- Startup
### Cấu trúc thư mục cho một dự án ASP.NET Core sử dụng Clean Architecture
``` pgsql
├── src
│   ├── Application
│   │   ├── Interfaces
│   │   │   ├── IOrderRepository.cs
│   │   │   ├── IProductRepository.cs
│   │   │   ├── IEmailService.cs
│   │   │   └── IDomainEventDispatcher.cs
│   │   ├── Services
│   │   │   ├── OrderService.cs
│   │   │   └── ProductService.cs
│   │   ├── Specifications
│   │   │   ├── OrderByStatusSpecification.cs
│   │   │   ├── OrderByDateRangeSpecification.cs
│   │   │   └── OrderByCustomerSpecification.cs
│   │   ├── Exceptions
│   │   │   ├── ProductNotFoundException.cs
│   │   │   ├── InsufficientStockException.cs
│   │   │   └── OrderNotFoundException.cs
│   │   ├── GuardClauses
│   │   │   └── Guard.cs
│   │   ├── DTOs
│   │   │   ├── OrderDto.cs
│   │   │   └── ProductDto.cs
│   ├── Domain
│   │   ├── Entities
│   │   │   ├── Order.cs
│   │   │   ├── OrderItem.cs
│   │   │   ├── Product.cs
│   │   │   └── Customer.cs
│   │   ├── Aggregates
│   │   │   ├── OrderAggregate.cs
│   │   │   └── ProductAggregate.cs
│   │   ├── ValueObjects
│   │   │   ├── Money.cs
│   │   │   ├── Address.cs
│   │   │   └── OrderStatus.cs
│   │   ├── Events
│   │   │   ├── OrderCreatedEvent.cs
│   │   │   └── OrderShippedEvent.cs
│   │   ├── EventHandlers
│   │   │   ├── SendOrderConfirmationEmailHandler.cs
│   │   │   ├── UpdateProductStockHandler.cs
│   │   │   └── SendOrderConfirmationSmsHandler.cs
│   ├── Infrastructure
│   │   ├── Persistence
│   │   │   ├── ApplicationDbContext.cs
│   │   │   ├── OrderRepository.cs
│   │   │   ├── ProductRepository.cs
│   │   │   └── CustomerRepository.cs
│   │   ├── Services
│   │   │   ├── EmailService.cs
│   │   │   ├── SmsService.cs
│   │   │   └── LoggingService.cs
│   │   ├── EventDispatcher
│   │   │   └── DomainEventDispatcher.cs
│   ├── Presentation (API Layer)
│   │   ├── Controllers
│   │   │   ├── OrdersController.cs
│   │   │   ├── ProductsController.cs
│   │   │   └── CustomersController.cs
│   │   ├── Middlewares
│   │   │   ├── ExceptionHandlingMiddleware.cs
│   │   │   ├── RequestLoggingMiddleware.cs
│   │   │   └── AuthenticationMiddleware.cs
│   ├── WebAPI
│   │   ├── Program.cs
│   │   ├── Startup.cs
│   │   ├── appsettings.json
│   │   ├── DependencyInjection.cs
│   │   ├── Logging.cs
│   │   └── Filters
│   │       ├── ValidationFilter.cs
│   │       ├── AuthorizationFilter.cs
│   │       └── ExceptionFilter.cs
├── tests
│   ├── Application.Tests
│   │   ├── OrderServiceTests.cs
│   │   ├── ProductServiceTests.cs
│   │   └── OrderSpecificationTests.cs
│   ├── Domain.Tests
│   │   ├── OrderTests.cs
│   │   ├── ProductTests.cs
│   │   ├── MoneyTests.cs
│   │   └── AddressTests.cs
│   ├── Infrastructure.Tests
│   │   ├── OrderRepositoryTests.cs
│   │   ├── ProductRepositoryTests.cs
│   │   └── EmailServiceTests.cs
```
###### **📌 Giải thích thư mục**

1️⃣ **Application Layer** (Lớp nghiệp vụ - Business Logic)

- **Chứa toàn bộ logic nghiệp vụ** nhưng **không phụ thuộc vào database hay UI**.
- **Services**: Xử lý logic nghiệp vụ (OrderService, ProductService).
- **Specifications**: Định nghĩa các tiêu chí lọc dữ liệu.
- **DTOs**: Chuyển đổi dữ liệu giữa các tầng.
- **Exceptions**: Chứa các ngoại lệ (Custom Exceptions).
- **Guard Clauses**: Chứa lớp `Guard.cs` để kiểm tra dữ liệu đầu vào.

2️⃣ **Domain Layer** (Lớp miền - Domain Logic)

- **Chứa các đối tượng cốt lõi của hệ thống, không phụ thuộc vào bất kỳ thứ gì khác**.
- **Entities**: Các thực thể chính (`Order`, `Product`, `Customer`).
- **Aggregates**: Các nhóm Entity có quan hệ chặt chẽ.
- **ValueObjects**: Đối tượng không có ID (`Money`, `Address`, `OrderStatus`).
- **Events & Handlers**: Xử lý sự kiện miền (`OrderCreatedEvent`, `SendOrderConfirmationEmailHandler`).

3️⃣ **Infrastructure Layer** (Lớp hạ tầng - Database, External Services)↳

- **Chứa các thành phần thực hiện dữ liệu**:
    - **Persistence**: Tương tác với database (`ApplicationDbContext`, `Repositories`).
    - **Services**: Các dịch vụ bên ngoài như email, logging, SMS.
    - **EventDispatcher**: Cơ chế phát sự kiện miền (`DomainEventDispatcher`).

4️⃣ **Presentation Layer (API Layer)**

- **Chứa tất cả các thành phần liên quan đến giao diện lập trình API**.
- **Controllers**: Giao tiếp với frontend hoặc các dịch vụ khác.
- **Middlewares**: Xử lý lỗi, log request, xác thực.
- **Filters**: Lọc dữ liệu và xử lý request đầu vào.

5️⃣ **Tests**

- **Kiểm thử tất cả các thành phần của hệ thống**.
- `Application.Tests`: Kiểm thử `OrderService`, `ProductService`.
- `Domain.Tests`: Kiểm thử logic của `Order`, `Product`.
- `Infrastructure.Tests`: Kiểm thử `OrderRepository`, `EmailService`.

---

##### **📌 Lợi ích của cách sắp xếp này**

✅ **Tách biệt các tầng** giúp dễ bảo trì và mở rộng.  
✅ **Không phụ thuộc vào framework cụ thể** (Entity Framework, API, UI).  
✅ **Hỗ trợ dễ dàng thay thế, mở rộng các thành phần** (Repository, Event Handlers, Services).  
✅ **Dễ kiểm thử** nhờ tách biệt Application, Domain và Infrastructure.