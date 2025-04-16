---
title: Routing
tags:
  - ASPnetCore
---
### Mục đích của Routing
- Routing cho phép ASP.NET Core Applications hướng các HTTP Requests tới các functions hay Controllers chính xác dựa trên URL patterns

### Core Routing Components
- ***Route parameters***: ***Dynamic placeholder*** như `{id}` giúp các route trở nên linh động hơn, hỗ trợ nhiều input khác nhau với một route duy nhất
- Optional parameters: Sử dụng kèm `?` , optional parameters cho phép các routes hoạt động ngay cả khi thiếu các data cụ thể, tăng tính linh động của route
- Constraints: Đảm bảo validate data bằng cách giới hạn kiểu và giá trị của route parameters
- Catch - all routes: The `{*filePath}` syntax captures all remaining segments in a path, helpful in serving files or content
- Query parameters: Các parameter nằm ngoài route, như `/search?q=aspnet&page=2`, giúp request mang lại nhiều thông tin hơn mà không làm thay đổi URL Structure
- EX: `user/{userID:int?}/{*extraInformation}`