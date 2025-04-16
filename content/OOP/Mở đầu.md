### Khái niệm về hệ thống
- Hệ thống là tập hợp các phần tử có liên hệ và cùng hướng tới một mục đích
![[Pasted image 20250324211423.png]]

### Phát triển hệ thống thông tin
- Xây dựng một hệ thống tốt:
	- Đáp ứng được các yêu cầu của NSD và tạo ra các giá trị cho tổ chức
- Phát triển hệ thống thông tin cần?
	- Hiểu được quy trình nghiệp vụ của hệ thống 
	- Hiểu nhu cầu của người dùng 
	- Có phương pháp, quy trình để phân tích và thiết kế các giải pháp

### SDLC
- **Lập kế hoạch (Planning)**
	-> Tại sao xây dựng hệ thống này (Why build the system?) 
- **Phân tích (Analysis)**
	-> Hệ thống cần làm gì? (Who, what, when, where will the system be?)
- **Thiết kế (Design)**
	-> Hệ thống cần thực hiện như thế nào? (How will the system work?)
- **Cài đặt (Implementation)**
	-> Xây dựng chương trình, triển khai, bảo trì, …


### Mô hình hóa
- Mô hình (Model):
	- **Mô hình** là sự trừu tượng hoá của một hệ thống phức tạp, tập trung vào những đặc điểm cốt lõi cần thiết để hiểu và giải quyết bài toán.
	- Chúng giúp giảm bớt sự phức tạp của hệ thống bằng cách loại bỏ những chi tiết không cần thiết.
	
- Mô hình hóa (Modeling):
	- Mô phỏng được hình ảnh tương tự của hệ thống
	- Đơn giản hóa hệ thống
	- Làm sáng tỏ vấn đề
	- Tập trung vào các khía cạnh cần quan tâm
	
- Yêu cầu chất lượng của một mô hình
	- **Abstraction:** Giữ lại những thông tin cốt lõi.
	- **Understandability (Dễ hiểu):** Trình bày trực quan để người đọc dễ nắm bắt.
	- **Accuracy (Chính xác):** Phản ánh đúng các đặc điểm quan trọng của hệ thống.
	- **Predictiveness (Dự đoán):** Cho phép dự đoán các hành vi của hệ thống qua mô phỏng hoặc phân tích.
	- **Cost-effectiveness (Hiệu quả về chi phí):** Chi phí tạo ra mô hình phải nhỏ hơn hoặc xứng đáng với lợi ích thu được khi triển khai hệ thống.
### Mô hình hóa hướng đối tượng
- Ý tưởng: Thế giới thực gồm các đối tượng có tương tác với nhau
- Cần mô hình hóa bài toán thành các đối tượng
![[Pasted image 20250324212237.png]]

### Ngôn ngữ mô hình hóa UML
- UML là một ngôn ngữ để mô hình hóa 
	- Các nguyên tắc và ký hiệu đã chuẩn hóa 
	- Biểu diễn và lưu trữ các mô hình
- Các đặc điểm của UML 
	- Phù hợp với mô hình hóa hướng đối tượng 
	- Mô hình trực quan 
	- Đặc tả rõ ràng, chính xác 
	- Làm tài liệu: mô tả yêu cầu, đặc tả 
	- ...

#### Giai đoạn phát triển
- Xác định nhu cầu (Requirement determination)
	- Các ca sử dụng (use case) để xác định các yêu cầu 
	- Biểu đồ ca sử dụng
- Phân tích (Analysis)
	- Biểu đồ lớp thể hiện cấu trúc tĩnh của hệ thống
	- Các biểu đồ trình tự, biểu đồ trạng thái thể hiện cấu trúc động 
- Thiết kế (Design)
	- Các lớp được mô hình hóa chi tiết với các phương thức 
- Cài đặt (Implementation)
	- Các mô hình UML có thể ánh xạ sang code

#### Các biểu đồ:
	Structured Diagrams
		class
		object
		component
		deployment
	Behavioral Diagrams
		use case
		sequence
		statechart
		activity