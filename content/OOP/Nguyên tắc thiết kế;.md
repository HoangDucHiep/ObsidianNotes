
## 1. Các khái niệm cơ bản trong OOP

- **Polymorphism (Đa hình):** Khả năng một giao diện chung có nhiều cách triển khai khác nhau.
    
- **Inheritance (Kế thừa):** Cho phép lớp con kế thừa thuộc tính và phương thức từ lớp cha.
    
- **Encapsulation (Đóng gói):** Che giấu chi tiết cài đặt, chỉ phơi bày giao diện tương tác.
    
- **Abstraction (Trừu tượng hóa):** Lấy ra những đặc điểm chung, bỏ qua chi tiết không cần thiết. ​
    

---

## 2. Nguyên tắc SOLID

1. **SRP – Single Responsibility Principle**  
    Mỗi lớp chỉ nên có **một** lý do duy nhất để thay đổi (một trách nhiệm duy nhất).
    
2. **OCP – Open/Closed Principle**  
    Lớp/module nên **mở** cho việc **mở rộng** nhưng **đóng** cho việc **sửa đổi**.
    
3. **LSP – Liskov Substitution Principle**  
    Đối tượng của lớp dẫn xuất có thể thay thế cho đối tượng lớp cơ sở mà không làm hỏng chương trình.
    
4. **ISP – Interface Segregation Principle**  
    Không buộc client phải phụ thuộc vào những phương thức mà nó không sử dụng; nên tách các interface lớn thành các interface nhỏ, chuyên biệt.
    
5. **DIP – Dependency Inversion Principle**  
    – Các thành phần cấp cao không phụ thuộc vào thành phần cấp thấp, mà cả hai cùng phụ thuộc vào abstraction.  
    – Abstraction không phụ thuộc vào details, mà details phụ thuộc vào abstraction. ​
    

---

## 3. Một số mẫu thiết kế GRASP (General Responsibility Assignment Software Patterns)

- **Low Coupling:** Giảm sự phụ thuộc lẫn nhau giữa các lớp để dễ bảo trì, tái sử dụng.
    
- **High Cohesion:** Giữ cho mỗi lớp chỉ chuyên trách các trách nhiệm liên quan chặt chẽ với nhau.
    
- **Information Expert:** Gán trách nhiệm cho lớp nào “biết” đủ thông tin để thực thi tốt nhất.
    
- **Creator:** Xác định lớp nào chịu trách nhiệm tạo đối tượng của lớp khác dựa trên mối quan hệ “chứa” hoặc “sử dụng”.
    
- **Polymorphism (trong GRASP):** Sử dụng đa hình để phân tán trách nhiệm cho các lớp con, tránh các điều kiện rẽ nhánh dựa trên kiểu. ​