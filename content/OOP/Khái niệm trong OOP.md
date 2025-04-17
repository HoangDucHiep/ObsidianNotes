### Classes (Lớp)
- Định nghĩa trừu tượng, các thuộc tính, hành vi của tập hợp các đối tượng có chung đặc điểm
- Ví dụ: Lớp Person có thể chứa các thuộc tính như tên, địa chỉ và hành vi như đăng ký hoặc cập nhật thông tin.![[Pasted image 20250324213903.png]]
- Tác dụng của lớp? 
	- Trừu tượng hoá dữ liệu (data abstraction) 
	- Bao gói (encapsulation): dữ liệu + thao tác 
	- Che giấu thông tin (information hiding)
### Object (Đối tượng)
- Đối tượng là các thể hiện cụ thể (instance) của lớp, có bản sắc riêng và trạng thái riêng biệt.
- Mỗi đối tượng được xác định bởi giá trị của các thuộc tính và có thể thực hiện các hành động được định nghĩa trong lớp.
- Một đối tượng gồm những gì? 
	- Định danh (identity): mỗi đối tượng là duy nhất trong bộ nhớ 
	- Trạng thái (state): định hình bởi giá trị các thuộc tính của đối tượng 
	- Ứng xử (behaviour): thể hiện bởi các hành động có thể của đối tượng

### Message (Thông điệp)
- Các đối tượng giao tiếp với nhau qua việc gửi và nhận thông điệp, yêu cầu thực hiện các thao tác.
- Cơ chế này cho phép các đối tượng tương tác mà không cần biết chi tiết về cách thức hoạt động của nhau.![[Pasted image 20250324214043.png]]
- Phương thức VS Thông điệp:
	- **Phương thức (method)** là hàm thành phần của lớp (member function)
	- **Thông điệp** là ***lời gọi hàm*** của một đối tượng của lớp đó


### Inheritance (Kế thừa)
- Cho phép một lớp (subclass) kế thừa các thuộc tính và hành vi của lớp khác (superclass).
- Tạo ra mối quan hệ phân cấp, giảm thiểu sự lặp lại mã và tăng khả năng tái sử dụng.![[Pasted image 20250324214204.png]]
### Encapsulation (Đóng gói)
- Kỹ thuật ẩn giấu thông tin nội bộ của đối tượng khỏi truy cập trực tiếp từ bên ngoài, chỉ cho phép truy cập thông qua các giao diện được định nghĩa rõ ràng (public, private, protected).
- Giúp bảo vệ trạng thái nội bộ và đảm bảo an toàn cho dữ liệu.

### Polymorphism (Đa hình)
- Cho phép một biến hoặc phương thức có thể thể hiện nhiều hình thái khác nhau tùy vào ngữ cảnh hoặc kiểu đối tượng cụ thể.
- Bao gồm các hình thức như genericity, overloading, và dynamic binding giúp linh hoạt trong việc xử lý các đối tượng thuộc các lớp khác nhau.
![[Pasted image 20250324214315.png]]

## Các kiểu liên kết
### Association
- Các đối tượng của hai lớp có thể tương tác với nhau (thông qua truyền thông điệp – message passing)
- Liên kết có thể được ghi rõ 
- Đôi khi có thể ghi rõ vai trò (role name) ở mỗi đầu liên kết
![[Pasted image 20250415154351.png]]
![[Pasted image 20250415154359.png]]

### Aggregation
- Thể hiện quan hệ tổng thể - thành phần (whole-part) 
- Trong mô tả thường có các cụm từ: “gồm có” (consist of), “có một” (has a), “là một phần của” (is a part of)
![[Pasted image 20250415154433.png]]

### Composition
- Là một dạng quan hệ tổng thể - thành phần 
- Mạnh hơn quan hệ kết tập, trong đó ***các thành phần không tồn tại riêng rẽ*** với tổng thể
![[Pasted image 20250415154518.png]]
![[Pasted image 20250415154642.png]]



### Thế nào là một lớp tốt:
1. Problem domain: Trong quá trình phân tích, các lớp nên phản ánh đúng các đối tượng trong phạm vi của bài toán 
2. Functionality: Một lớp cần có cả dữ liệu và các hành vi (ít nhất là trong quá trình phân tích). Nếu một lớp chỉ có các hành vi thì nó nên thuộc vào các lớp khác. Một lớp cũng không nên chỉ có các thuộc tính (dù có thể có thêm một số hàm set/get) 
3. Cohesion: Mỗi lớp nên có tính cố kết cao, chỉ nên liên quan đến một việc chính 
4. Substituability: Khi có kế thừa, đối tượng của lớp dẫn xuất (lớp con) cần có thể thay thế được cho một đối tượng của lớp cơ sở (lớp cha)



### Các câu hỏi:
#### 1. Các đặc trưng của một đối tượng
- Các định danh (identity): Mỗi đối tượng là duy nhất trong bộ nhớ
- Trạng thái (state): Định hình bởi các giá trị của các thuộc tính của đối tượng
- Ứng xử (behaviour): thể hiện bởi các hành động có thể của đối tượng

#### 2. Sự khác nhau giữa đối tượng và lớp? Ký hiệu UML của chúng thế nào? 
- Lớp là một định nghĩa trừu tượng của các đối tượng có cùng những đặc tính chung trong thực tế
- Đối tượng là một instance của Lớp, có đặc trưng và trạng thái riêng biệt.

#### 3. Các đối tượng giao tiếp với nhau bằng cách nào?
- Thống qua việc gửi và nhận thông điệp, yêu cầu thực hiện các thao tác.
- Cơ chế này cho phép các đối tượng tương tác mà không cần biết chi tiết về cách thức hoạt động của nhau.
#### 4. Liệt kê 4 loại liên kết giữa các lớp?
- Association
- Aggregation
- Composition
- Inheritance
#### 5. Khác nhau giữa kết hợp (association) và kết tập (aggregation)
- **Kết hợp (Association)**:
	- Là một mối quan hệ tổng quát giữa hai lớp, cho phép các đối tượng của hai lớp tương tác với nhau.
- **Kết tập (Aggregation)**:
	- Là một dạng đặc biệt của kết hợp, thể hiện mối quan hệ "tổng thể - thành phần" (whole-part).
#### 6. Khác nhau giữa kết tập (aggregation) và gộp (composition)?
- Đều  là mối quan hệ thổng thể, thành phần, nhưng composition mạnh hơn, khi các thành phần trong aggregation, còn trong composition thì không
#### 7. Khi nào có thể mô hình một lớp là lớp con của một lớp khác?
- Một lớp có thể được mô hình hóa là lớp con của một lớp khác khi có mối quan hệ **"is-a"** (là một loại của) giữa chúng. Điều này có nghĩa là lớp con là một phiên bản cụ thể hơn của lớp cha và kế thừa các thuộc tính cũng như hành vi của lớp cha.
#### 8. Sự khác nhau giữa một hoạt động (operation) và một phương thức (method)? 
- **Hoạt động (Operation)**:
	- Là một khái niệm trừu tượng, mô tả một hành động hoặc chức năng mà một lớp có thể thực hiện.
	- Không chỉ rõ cách thực hiện, mà chỉ định nghĩa rằng lớp có khả năng thực hiện hành động đó.
	- Ví dụ: Một lớp "Hình học" (Shape) có thể có một hoạt động là "tính diện tích" (calculateArea).
- **Phương thức (Method)**:
	- Là cách cụ thể mà một hoạt động được thực hiện trong một lớp.
	- Phương thức là hiện thực (implementation) của hoạt động, bao gồm mã nguồn để thực hiện hành động đó.
	- Ví dụ: Trong lớp "Hình tròn" (Circle), phương thức `calculateArea()` sẽ chứa công thức tính diện tích hình tròn: `π * r^2`.
#### 9. Một số tiêu chuẩn thiết kế của một lớp được coi là tốt
1. Problem domain: Trong quá trình phân tích, các lớp nên phản ánh đúng các đối tượng trong phạm vi của bài toán 
2. Functionality: Một lớp cần có cả dữ liệu và các hành vi (ít nhất là trong quá trình phân tích). Nếu một lớp chỉ có các hành vi thì nó nên thuộc vào các lớp khác. Một lớp cũng không nên chỉ có các thuộc tính (dù có thể có thêm một số hàm set/get) 
3. Cohesion: Mỗi lớp nên có tính cố kết cao, chỉ nên liên quan đến một việc chính 
4. Substituability: Khi có kế thừa, đối tượng của lớp dẫn xuất (lớp con) cần có thể thay thế được cho một đối tượng của lớp cơ sở (lớp cha)
####  10. Lớp trừu tượng là gì:
	Lớp trừu tượng (abstract class) là một loại lớp trong lập trình hướng đối tượng được sử dụng để định nghĩa các đặc điểm chung cho các lớp con, nhưng bản thân nó không thể tạo ra đối tượng trực tiếp. Lớp trừu tượng thường được sử dụng để làm nền tảng cho một hệ thống phân cấp kế thừa, nơi các lớp con cụ thể kế thừa và triển khai các chức năng được định nghĩa trong lớp trừu tượng.

#### Nối 

| **Concept**    | **Definition**                                                              |
| -------------- | --------------------------------------------------------------------------- |
| Aggregation    | Whole-part relationship                                                     |
| Association    | Relationship between classes                                                |
| Attribute      | Data item defined as part of a class or object                              |
| Class          | Template for objects                                                        |
| Data hiding    | Concealing internal details of an object                                    |
| Encapsulation  | Packaging together data and operations                                      |
| Generalization | Abstracting common features into a superclass                               |
| Inheritance    | A relationship between two classes where one is a specialization of another |
| Instantiation  | Creation of an object                                                       |
| Message        | Request for a service to be executed                                        |
| Method         | Code implementing an operation                                              |
| Object         | Instance of a class                                                         |
| Operation      | Interface of a method                                                       |
| Polymorphism   | The ability of one operation to be implemented by different methods         |

#### 1. Hãy nêu tầm quan trọng của mô hình hóa cấu trúc hệ thống (structural modeling)?
- **Hiểu rõ thành phần và cấu trúc của hệ thống**:
- **Hỗ trợ tổ chức và quản lý hệ thống**:
- **Phát hiện lỗi sớm trong giai đoạn thiết kế**:
- **Hỗ trợ lập trình hướng đối tượng**:

#### 2. Các bước chính để xây dựng biểu đồ lớp?
- Xác định đối tượng và lớp
- Xác định các thuộc tính của từng lớp
- Xác định mối quan hệ giữa các lớp
- Xác định trách nhiệm của từng lớp

#### 3. Liệt kê các loại đối tượng thường gặp
- **Người (People)**: Các cá nhân hoặc nhóm người tham gia vào hệ thống, ví dụ: người dùng, nhân viên, khách hàng.
- **Tổ chức (Organizations)**: Các tổ chức hoặc nhóm có vai trò quan trọng trong hệ thống, ví dụ: công ty, đội nhóm, cơ quan.
- **Đồ vật (Physical things)**: Các thực thể vật lý mà hệ thống cần quản lý hoặc tương tác, ví dụ: thiết bị, sản phẩm, tài sản.
- **Khái niệm (Conceptual things)**: Các ý tưởng hoặc khái niệm trừu tượng liên quan đến hệ thống, ví dụ: giao dịch, hợp đồng, sự kiện.
#### 4. Liệt kê 4 loại quan hệ chính giữa các lớp?
- Kết hợp (Association)
- Kết tập (Aggregation)
- Gộp (Composition)
- Kế thừa (Inheritance)

#### 5. Trình bày các lý do để loại bỏ một lớp ứng viên khi tìm lớp?
- ***Các thuộc tính***: số xe, loại xe, kiểu dáng, kích thước, nhà sản xuất, phí thuê mỗi ngày, tiền đặt cọc, ngày bắt đầu, thời gian dự kiến, ngày trả, các chi tiết bổ sung về các xe chuyên biệt
- ***Sự trùng lặp*** 
	- lịch sử thuê xe = lịch sử thuê xe trong quá khứ
	- danh sách các xe: có lớp xe là đủ
- ***Không rõ ràng*** 
	- sự trả lại xe (không rõ định nói chính xác cái gì)
- ***Liên quan các khái niệm vào/ra vật lý*** 
- ***Bên ngoài phạm vi hệ thống*** 
- ***Là toàn bộ hệ thống*** 
- ***Các liên kết***
	- Nếu các liên kết cần có thông tin kèm theo, ví dụ thuê (ngày, giá…)
#### 6. Tại sao những khái niệm như Hire lại được mô hình như một lớp thay vì là một liên kết?
- **Chứa thông tin bổ sung**:
    - Một liên kết chỉ biểu diễn mối quan hệ giữa các đối tượng, nhưng lớp **Hire** cần lưu trữ các thông tin như ngày thuê, thời gian dự kiến, phí thuê, tiền đặt cọc, trạng thái của xe, và các chi tiết khác. Những thông tin này không thể được biểu diễn trong một liên kết đơn giản.
- **Có hành vi riêng**:
    - Lớp **Hire** có thể bao gồm các phương thức để tính toán phí thuê, xử lý trả xe, hoặc ghi nhận lịch sử thuê. Những hành vi này cần được định nghĩa trong một lớp riêng biệt.
- **Quản lý mối quan hệ phức tạp**:
    - Một khách hàng có thể thuê nhiều xe, và mỗi xe có thể có thời hạn thuê khác nhau. Lớp **Hire** giúp quản lý mối quan hệ này một cách rõ ràng và có tổ chức.
- **Tăng tính mở rộng và tái sử dụng**:
    - Khi mô hình hóa **Hire** thành một lớp, hệ thống có thể dễ dàng mở rộng để thêm các tính năng mới liên quan đến việc thuê, như quản lý trạng thái thuê hoặc tích hợp với hệ thống thanh toán.
- **Đảm bảo tính kết dính (cohesion)**:
    - Nếu thông tin thuê được lưu trữ trong lớp **Customer** hoặc **Vehicle**, các lớp này sẽ trở nên cồng kềnh và mất đi tính kết dính. Việc tạo lớp **Hire** riêng biệt giúp duy trì sự rõ ràng và tổ chức trong thiết kế.

####
![[Pasted image 20250417003503.png]]

