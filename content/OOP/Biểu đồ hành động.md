### Biểu đồ hành động
- Là công cụ để mô hình các quá trình phức tạp gồm nhiều bước thực hiện
- Biểu đồ hành động thường dùng để mô tả
	- Luồng công việc (Workflow) của hệ thống
	- Những hành động trong từng kịch bản của ca sử dụng
	- Các chi tiết hoạt động của một chức năng
	- Các thuật toán phức tạo
- ![[Pasted image 20250415152153.png]]
- ![[Pasted image 20250415152328.png]]
- ![[Pasted image 20250415152335.png]]
- ![[Pasted image 20250415152341.png]]
- ![[Pasted image 20250415152346.png]]
- ![[Pasted image 20250415152356.png]]
- ![[Pasted image 20250415152412.png]]



### Trả lời các câu hỏi
### 1. Mục đích của biểu đồ hành động (activity diagram) là gì?
- là công cụ để mô hình các quá trình phức tạp gồm nhiều bước thực hiện
### 2. Những loại quá trình nào có thể được mô tả bằng biểu đồ hành động?
- Luồng công việc (workflow) của hệ thống 
- Những hành động trong từng kịch bản của ca sử dụng 
- Các chi tiết hoạt động của một chức năng 
- Các thuật toán phức tạp
### 3. So sánh biểu đồ hành động và sơ đồ khối (flowchart) (Chat)
Biểu đồ hành động (Activity Diagram) và sơ đồ khối (Flowchart) đều là công cụ trực quan để mô tả quy trình, nhưng chúng có những điểm khác biệt rõ rệt:
##### **Biểu đồ hành động (Activity Diagram):**
- **Mục đích:** Được sử dụng trong phân tích và thiết kế hệ thống hướng đối tượng (UML), tập trung vào mô tả luồng công việc hoặc các hoạt động trong hệ thống.
- **Ký hiệu:** Bao gồm các thành phần như trạng thái, hành động, điều kiện, vòng lặp, và các swimlane để phân biệt vai trò hoặc đối tượng tham gia.
- **Ứng dụng:** Thường dùng để mô tả quy trình nghiệp vụ, các kịch bản của ca sử dụng (use case), hoặc các thuật toán phức tạp.
- **Đặc điểm:** Có thể mô tả các hoạt động song song và tương tác giữa các đối tượng.
##### **Sơ đồ khối (Flowchart):**
- **Mục đích:** Là công cụ phổ biến để mô tả quy trình, thuật toán hoặc hệ thống một cách đơn giản, không nhất thiết phải liên quan đến lập trình hướng đối tượng.
- **Ký hiệu:** Sử dụng các hình học cơ bản như hình chữ nhật (hành động), hình thoi (điều kiện), và mũi tên (luồng dữ liệu).
- **Ứng dụng:** Thích hợp để minh họa các thuật toán, quy trình công việc đơn giản hoặc các bước xử lý trong lập trình.
- **Đặc điểm:** Dễ hiểu, không yêu cầu quy tắc nghiêm ngặt về notation như biểu đồ hành động.
##### **Điểm khác biệt chính:**
- Biểu đồ hành động có tính năng mô tả chi tiết hơn về các trạng thái và tương tác trong hệ thống, trong khi sơ đồ khối tập trung vào việc trình bày các bước tuần tự của quy trình.
- Biểu đồ hành động thường được sử dụng trong thiết kế phần mềm, còn sơ đồ khối phù hợp với các lĩnh vực khác như giáo dục, quản lý, hoặc kỹ thuật.
### 4. Những yếu tố nào trong hầu hết các ngôn ngữ lập trình có thể được mô tả trong biểu đồ hành động?
Biểu đồ hành động có thể mô tả một số yếu tố cơ bản của hầu hết các ngôn ngữ lập trình, bao gồm:

##### **1. Luồng công việc (Workflow):**
Mô tả cách các nhiệm vụ hoặc hành động diễn ra tuần tự hoặc song song, tương tự như cách các hàm (functions) hoặc các luồng xử lý trong chương trình hoạt động.
##### **2. Điều kiện và lựa chọn (Conditions and Decision-Making):**
Biểu đồ hành động sử dụng các ký hiệu để hiển thị các điều kiện (if/else, switch case), cho thấy các nhánh xử lý khác nhau dựa trên các giá trị hoặc trạng thái.
##### **3. Vòng lặp (Loops):**

Biểu thị các hoạt động lặp lại, như các vòng lặp for, while, hoặc do-while trong hầu hết các ngôn ngữ lập trình.

##### **4. Hành động song song (Parallel Actions):**
Mô tả các hoạt động thực hiện đồng thời, tương tự như lập trình đa luồng (multi-threading) hoặc xử lý song song.
##### **5. Tương tác với đối tượng hoặc cơ sở dữ liệu (Interactions with Objects or Databases):**
Thể hiện cách các đối tượng hoặc cơ sở dữ liệu được truy cập, sửa đổi hoặc sử dụng trong quy trình, giống như các thao tác CRUD (Create, Read, Update, Delete) trong lập trình.
##### **6. Chức năng hoặc quy trình (Functionality or Processes):**
Bao gồm các hành động hoặc thao tác cụ thể, tương tự như các hàm hoặc khối mã được gọi trong ngôn ngữ lập trình.
##### **7. Trạng thái (States):**
Mô tả các trạng thái mà hệ thống hoặc đối tượng có thể trải qua, tương tự như các trạng thái trong lập trình hướng đối tượng hoặc máy trạng thái (state machine).
##### **8. Swimlane (Vai trò hoặc đối tượng):**
Phân biệt các vai trò hoặc đối tượng tham gia vào quy trình, giống như việc chia quyền hoặc module trong một chương trình.