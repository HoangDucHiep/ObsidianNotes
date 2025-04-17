### 1. **Trình bày về các cách thức lưu trữ dữ liệu**

- **Tệp tin (File):** Lưu trữ đơn giản nhưng khó tổ chức, tìm kiếm và kiểm soát dữ liệu phức tạp.
- **Cơ sở dữ liệu hướng đối tượng (Object-Oriented Database):** Dữ liệu được lưu trữ dưới dạng đối tượng, phù hợp với các hệ thống hướng đối tượng nhưng ít phổ biến hơn.
- **Cơ sở dữ liệu quan hệ (Relational Database):** Dữ liệu được lưu dưới dạng bảng, dễ quản lý, phổ biến và được chuẩn hóa.
    
---

### 2. **Cơ sở dữ liệu quan hệ là gì?**
- Là hệ quản trị cơ sở dữ liệu tổ chức dữ liệu thành các **bảng (table)**.
- Mỗi bảng gồm các **bản ghi (record)** và **trường (field)**.
- Sử dụng **khóa chính (primary key)** để định danh duy nhất từng bản ghi.
- Dùng **khóa ngoại (foreign key)** để tạo mối quan hệ giữa các bảng.
- Có nền tảng lý thuyết vững chắc và được hỗ trợ bởi ngôn ngữ SQL.

---

### 3. **Chuyển một lớp thành bảng
- Mỗi **lớp** tương ứng với **một bảng**.
- Các **thuộc tính** của lớp trở thành **các cột (fields)** trong bảng.
- Mỗi **đối tượng** tương ứng với một **hàng (record)** trong bảng.

---

### 4. **Chuyển các lớp có liên kết 1-nhiều thành các bảng
- **Cách 1:** Tạo thêm một bảng trung gian để quản lý mối liên hệ.
- **Cách 2 (phổ biến hơn):** Thêm **khóa ngoại** vào bảng tương ứng với lớp phía “nhiều”.

---

### 5. **Chuyển các lớp có liên kết nhiều-nhiều thành các bảng
- Tạo **bảng trung gian** chứa:
    - Khóa ngoại từ hai bảng gốc.
    - Có thể thêm các thuộc tính liên quan đến mối quan hệ nếu cần.
- Biến liên kết n-n thành hai liên kết 1-nhiều.

---

### 6. **Chuyển các lớp có quan hệ kế thừa thành các bảng
Có **2 cách tiếp cận chính**:
- **Cách 1: Dùng một bảng chung
    - Một bảng chứa tất cả các thuộc tính của lớp cha và lớp con.
    - Có thể có nhiều ô **NULL** (vì không phải lớp con nào cũng dùng hết các cột).
- **Cách 2: Dùng nhiều bảng**
    - Mỗi lớp (cha hoặc con) có một bảng riêng.
    - Các bảng con có khóa ngoại trỏ đến bảng cha.
    - Cách này **tối ưu về chuẩn hóa** nhưng có thể sinh nhiều bảng hơn.