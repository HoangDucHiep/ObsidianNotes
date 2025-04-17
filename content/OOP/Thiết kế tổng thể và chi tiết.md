
### 1. **Đường điều hướng (navigable path) là gì?**
Đường điều hướng là cách chỉ định hướng mà một đối tượng có thể truy cập hoặc gửi thông điệp đến một đối tượng khác trong mô hình. Nếu có đường điều hướng từ A đến B, thì A có thể gọi các phương thức hoặc truy cập thuộc tính của B.

---
### 2. **Ý nghĩa của điều hướng một chiều?**
Điều hướng một chiều có nghĩa là một đối tượng A có thể truy cập đến đối tượng B, nhưng ngược lại thì không. Điều này làm giảm sự phụ thuộc lẫn nhau và giúp hệ thống dễ bảo trì hơn.

---
### 3. **Nêu khác biệt giữa mô hình phân tích và mô hình thiết kế?**

|Mô hình|Mục tiêu|Đặc điểm|
|---|---|---|
|**Phân tích**|Xác định _"cái gì"_ cần xây dựng|Tập trung vào yêu cầu chức năng, độc lập với cài đặt|
|**Thiết kế**|Xác định _"làm sao"_ để xây dựng|Bao gồm yêu cầu chức năng và phi chức năng, phụ thuộc vào công nghệ và môi trường triển khai|

---
### 4. **Kiến trúc phân tầng (layered architecture) là gì?**
Là cách tổ chức hệ thống thành các tầng (layers) độc lập theo chức năng, như:
- Tầng giao diện người dùng (UI)
- Tầng xử lý nghiệp vụ (Business Logic)
- Tầng truy xuất dữ liệu (Data Access)  
    Mỗi tầng chỉ giao tiếp với tầng liền kề, giúp hệ thống dễ bảo trì và mở rộng.
    
---
### 5. **Biểu đồ gói (package diagram) dùng làm gì?**
Biểu đồ gói dùng để:
- Nhóm các phần tử mô hình (lớp, ca sử dụng…) thành các gói có liên quan.
- Thể hiện cấu trúc logic của hệ thống.
- Giúp quản lý và tổ chức mã nguồn hiệu quả.

---
### 6. **Sự phụ thuộc (dependency) giữa các gói là gì?
Một gói **B phụ thuộc gói A** nếu:
- Sự thay đổi trong gói A có thể ảnh hưởng đến hoạt động của gói B.
- Ví dụ: một lớp trong gói B gọi đến phương thức hoặc sử dụng lớp trong gói A.

---
### 7. **Biểu đồ thành phần (component diagram) dùng làm gì?
Biểu đồ thành phần mô tả:
- Cấu trúc phần mềm vật lý.
- Các thành phần phần mềm (file mã nguồn, thư viện, dữ liệu…).
- Mối quan hệ phụ thuộc giữa các thành phần.

---
### 8. **Biểu đồ triển khai (deployment diagram) dùng làm gì?**
Biểu đồ triển khai mô tả:
- Cấu trúc vật lý của hệ thống khi triển khai.
- Cách các thành phần phần mềm được phân bố trên các phần tử phần cứng (server, client, thiết bị...).