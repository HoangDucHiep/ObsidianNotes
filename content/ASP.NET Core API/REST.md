---
title: REST
tags:
  - Full-Stack
  - HTTP
date: 2/16/2025
---
![[rest_api.svg]]

> [!Definition] Definition
> <span style="color:rgb(184, 123, 234)">REST - REpresentation State Transfer</span>, là một kiến trúc cung cấp tiêu chuẩn giữa các hệ thống máy tính trên Web, giúp việc giao tiếp giữa chúng trở nên dễ dàng hơn
- Các hệ thống tuân thủ REST, được gọi là các hệ thống Restful, đặc trưng bởi cách chúng <span style="color:rgb(184, 123, 234)">stateless</span> và <span style="color:rgb(184, 123, 234)">tách biệt mối quan tâm giữa client và server</span>.

### <span style="color:rgb(184, 123, 234)">Separation of Client and Server
</span> 
- Với REST architectural style, implementation của client và server có thể được thực hiện một cách <span style="color:rgb(133, 255, 135)">độc lập</span> mà <span style="color:rgb(133, 255, 135)">không cần  quan tâm đến nhau</span>
- Miễn là 2 bên biết định dạng message để gửi cho nhau, ta có thể đạt được modular và separate, cải thiện tính linh hoạt, cross platforms, và khả năng mở rộng.
- Bằng cách sử dụng REST interface, clients khác nhau dùng gọi endpoints, thực hiện cùng một hành động sẽ nhận được các câu trả lời giống nhau.
### <span style="color:rgb(184, 123, 234)">Statelessness</span>
- Các hệ thống theo mô hình REST là <span style="color:rgb(184, 123, 234)">stateless</span>, nghĩa là ***server*** không cần biết bất cứ điều gì về trạng thái của ***clients*** và ***ngược lại***. 
- Theo cách này, cả máy chủ và máy khách đều có thể hiểu bất kỳ ***message*** nào nhận được, ngay cả khi không nhìn thấy các ***message*** trước đó. 
- Ràng buộc về trạng thái này được thực thi thông qua việc sử dụng các <span style="color:rgb(184, 123, 234)">resources</span>, thay vì ***commands***. 
> [!NOTE]
> <span style="color:rgb(184, 123, 234)">Resources</span> là một danh từ của web - chúng mô tả bất kỳ object, document hoặc vật nào mà bạn có thể cần lưu trữ hoặc gửi đến các dịch vụ khác
- Bởi vì các hệ thống REST tương tác thông qua các hoạt động tiêu chuẩn về Resources, chúng không dựa vào implementation of interfaces
- These constraints help RESTful applications achieve reliability, quick performance, and scalability, as components that can be managed, updated, and reused without affecting the system as a whole, even during operation of the system.
### <span style="color:rgb(184, 123, 234)">Communication between Client and Server</span> 
##### Request
- Một Request gồm:
	- HTTP verb: xác định loại hoạt động cần thực hiện
	- Header: cho phép client chuyển các thông tin của request
	- Path: tới resource
	- Optional message body chứa data
##### HTTP Verbs
- GET: lấy một resource cụ thể (by id, ...) hoặc một collection of rescource
- POST: tạo một resource mới
- PUT: update một resource cụ thể
- DELETE: remove một resource cụ thể

##### Header and Accept parameters
- Trong Header của một request, client gửi loại content mà nó có thể chấp nhận từ server, thông qua `Accept` field
- Các types:
	- `image` — `image/png`, `image/jpeg`, `image/gif`
	- `audio` — `audio/wav`, `audio/mpeg`
	- `video` — `video/mp4`, `video/ogg`
	- `application` — `application/json`, `application/pdf`, `application/xml`, `application/octet-stream`
- VD: For example, a client accessing a resource with `id` 23 in an `articles` resource on a server might send a GET request like this:
```
GET /articles/23
Accept: text/html, application/xhtml
```

##### Response
- Content types: 