### 1. Tổng Quan về Use Case Diagram
- Mô tả các kịch bản sử dụng (use cases) mà hệ thống cần thực hiện, tức là các chức năng hay dịch vụ mà hệ thống phải cung cấp cho người sử dụng, dưới góc nhìn của người dùng
- Xác định được “ai” (actors) sẽ tương tác với hệ thống và “điều gì” (use cases) mà họ thực hiện.
- Tác dụng:
	- Mô tả yêu cầu của người dùng
	- Mô tả tương tác giữa người sử dụng và hệ thống
	- Hiểu rõ ràng và nhất quán cái mà hệ thống cần làm
	- Cung cấp cơ sở để phân tích, thiết kế và kiểm thử hệ thống
        
- **Vai trò trong phát triển phần mềm:**
    - Là công cụ giao tiếp giữa khách hàng và đội ngũ phát triển, giúp chuyển giao yêu cầu của khách hàng thành các mô tả chức năng rõ ràng.
    - Là cơ sở để phát triển các bước phân tích và thiết kế chi tiết sau này.
---

### 2. Các Thành Phần Cơ Bản
##### a. Actors (Diễn viên)
- Định nghĩa: Đại diện cho vai trò hoặc đối tượng bên ngoài (có thể là con người, hệ thống khác, tổ chức…) tương tác với hệ thống.
- Các điểm chú ý:
	- Không nhất thiết phải là cá nhân cụ thể mà có thể là một nhóm hay một vai trò tổng quát (ví dụ: “Customer” hay “Admin”).
    - Mỗi actor có thể tham gia vào một hoặc nhiều use case.
    ![[Pasted image 20250324222522.png]]
 - Các loại actors:![[Pasted image 20250324222546.png]]
	- **Theo tính chất và vai trò:**
	    - **Human vs. Non-human:**
	        - Actor có thể là con người (ví dụ: Student, Professor) hoặc các hệ thống khác như máy chủ email.
	        - Thậm chí, các actor không phải con người cũng có thể được vẽ bằng hình stick figure.
	            
	    - **Active vs. Passive:**
	        - **Actor chủ động (active):** Là actor khởi tạo và tương tác trực tiếp với hệ thống để kích hoạt các use case.
	            - Ví dụ: Professor là actor chủ động khi thực hiện các tác vụ như truy vấn dữ liệu sinh viên, thông báo kỳ thi, hoặc phát hành chứng chỉ.
	        - **Actor bị động (passive):** Là actor không trực tiếp khởi tạo use case mà cung cấp dịch vụ, dữ liệu hỗ trợ cho quá trình thực hiện use case.
	            - Ví dụ: E-Mail Server có thể được xem là actor bị động, vì nó không nhận được lợi ích trực tiếp từ use case mà chỉ cung cấp chức năng hỗ trợ cho việc gửi thông báo.
	                
	- **Theo vai trò về lợi ích (Primary vs. Secondary):**
	    - **Primary Actor:** Nhận được lợi ích trực tiếp từ việc thực hiện use case.
	        - Ví dụ: Professor trong use case “Inform student” nếu họ nhận được thông tin phản hồi hay tiện ích từ hệ thống.
	    - **Secondary Actor:** Không nhận được lợi ích trực tiếp, mà chỉ tham gia hỗ trợ cho quá trình thực hiện use case.
	        - Ví dụ: E-Mail Server trong cùng use case, mặc dù tham gia quan trọng, nhưng không nhận được lợi ích trực tiếp từ quá trình đó.
	- **Lưu ý:**
	    - Mặc dù có các phân loại như trên, trên sơ đồ use case không có biểu hiện đồ họa phân biệt rõ ràng giữa actor chủ động, bị động, primary hay secondary.
	    - Actor luôn được xem là thực thể bên ngoài hệ thống. Dữ liệu hoặc thông tin về actor có thể được lưu trữ trong hệ thống (ví dụ: dưới dạng lớp trong sơ đồ lớp), nhưng actor bản thân không phải là một thành phần nội bộ của hệ thống.
##### b. Use cases (Ca sử dụng)
- **Định nghĩa:** Mô tả một chức năng hoặc dịch vụ mà hệ thống cung cấp để tạo ra giá trị cho actor.
- **Đặc điểm quan trọng:**
    - Mỗi use case được thể hiện dưới dạng một hình ellipse chứa tên của chức năng.
    - Use case thể hiện các kịch bản giao tiếp giữa hệ thống và actor mà không đi sâu vào chi tiết triển khai.
![[Pasted image 20250324221623.png]] Student Administration system, có 3 use cases: (1) Query student data, (2) Issue certificate, and (3) Announce exam.
##### c. Associations (Quan hệ)
- **Định nghĩa:** Đường nối giữa actor và use case biểu diễn mối quan hệ tương tác.
- **Các mối liên hệ khác:**
    - **Include (Bao gồm):** Một use case luôn luôn bao gồm việc thực hiện một use case khác như một phần của quy trình.
    - **Extend (Mở rộng):** Cho phép một use case mở rộng hành vi của một use case cơ sở khi có điều kiện đặc biệt.
    - **Generalization (Kế thừa):** Cho phép các use case (hoặc actor) con kế thừa các thuộc tính từ use case (hoặc actor) cha.![[Pasted image 20250324222810.png]]![[Pasted image 20250324222907.png]]
    - ![[Pasted image 20250324235434.png]]


### Mô tả ca sử dụng
![[Pasted image 20250414223235.png]]
VD: ![[Pasted image 20250414223303.png]]
![[Pasted image 20250414223312.png]]



### Câu hỏi:
##### 1. Mô hình ca sử dụng bao gồm những gì:
- Actors(Tác nhân) và mô tả tác nhân
- Use case description(Mô tả ca sử dụng)
- Use case diagram (Biểu đồ ca sử dụng)
- Scenarios (Tập các kịch bản)
##### 2. Nêu 2 cách để xác định các ca sử dụng?
- Có 2 cách là thông qua: 
	- Các tác nhân (Actors)
		- Tìm các tác nhân của hệ thống
		- Tìm các nhiệm vụ và chức năng mà tác nhân sẽ thi hành
		- Mô hình hóa mỗi nhiệm vụ chính thành một ca sử dụng
	- Các kịch bản (Scenarios)
		- Xem hệ thống họa động thế nào để xác định các các ca sử dụng
		- Mỗi ca sử dụng thể hiện một nhóm các kịch bản có cùng mục tiêu
##### 3. Nêu mối quan hệ giữa các kịch bản và ca sử dụng?
- Mối quan hệ giữa các kịch bản (scenarios) và ca sử dụng (use cases) là một sự liên kết chặt chẽ trong mô hình ca sử dụng. Cụ thể:
	1. **Kịch bản là các tình huống cụ thể trong ca sử dụng**:
	    - Ca sử dụng là mô tả tổng quan về một tập các tương tác giữa người dùng (hoặc hệ thống khác) với hệ thống cần xây dựng.
	    - Kịch bản là các trường hợp cụ thể thể hiện cách ca sử dụng hoạt động trong từng hoàn cảnh nhất định. Các kịch bản mô tả chi tiết dòng sự kiện (chính và phụ) của ca sử dụng.
	    
	2. **Kịch bản giúp mô tả ca sử dụng rõ ràng hơn**:
	    - Trong mô tả ca sử dụng, thường bao gồm phần dòng sự kiện chính (Typical course of events) và dòng sự kiện phụ (Alternative courses). Đây chính là các kịch bản, làm rõ các trường hợp sử dụng khác nhau của hệ thống.
	        
	3. **Kịch bản hỗ trợ xác định ca sử dụng**:
	    - Các kịch bản thực tế hoặc tưởng tượng có thể được dùng để xác định các ca sử dụng cần thiết trong hệ thống, dựa trên nhu cầu và hành vi của người dùng.
Ví dụ: Một kịch bản “Annie gọi đến cửa hàng để đặt lịch hẹn làm tóc” sẽ dẫn đến việc xác định ca sử dụng “Đặt lịch hẹn”.


##### 4. “Chức năng” như thế nào thì được coi là một “ca sử dụng”?
- Thể hiện dưới góc nhìn từ bên ngoài của người dùng về các chức năng hệ thống cần thực hiện
- Mỗi ca sử dụng thể hiện một nhiệm vụ chính hoặc một nhóm các chức năng chính của hệ thống
- Mỗi ca sử dụng phải liên kết với một hoặc một số tác nhân, trong đó có một tác nhân chính
- Mỗi ca sử dụng phải dẫn tới một số kết quả cụ thể
##### 5. Ca sử dụng được xây dựng trong những pha nào?
- **Phân tích yêu cầu**:
    - Trong giai đoạn này, các ca sử dụng được xác định dựa trên yêu cầu của người dùng và các tác nhân liên quan. Đây là bước đầu tiên để hiểu rõ hệ thống cần thực hiện những nhiệm vụ gì.
- **Thiết kế hệ thống**:
    - Ca sử dụng được mô hình hóa chi tiết hơn, bao gồm việc xây dựng biểu đồ ca sử dụng và mô tả các kịch bản liên quan. Điều này giúp đội ngũ phát triển hiểu rõ cách hệ thống sẽ tương tác với các tác nhân.
- **Thực hiện và kiểm thử**:
    - Các ca sử dụng được sử dụng để thiết kế và kiểm thử các chức năng của hệ thống, đảm bảo rằng mỗi ca sử dụng đáp ứng được mục tiêu ban đầu đặt ra.
- **Duy trì và phát triển**:
    - Trong quá trình nâng cấp hoặc duy trì hệ thống, các ca sử dụng có thể được xem xét và hiệu chỉnh để phù hợp với các yêu cầu mới hoặc cải tiến.

##### 6. Mô tả rút gọn ca sử dụng (high-level use case description) là gì?
![[Pasted image 20250414230047.png]]
- **Mô tả rút gọn ca sử dụng (high-level use case description)** là cách diễn đạt tổng quát về một ca sử dụng, tập trung vào các yếu tố cốt lõi mà không đi vào chi tiết cụ thể. Mục tiêu chính của mô tả này là cung cấp cái nhìn tổng quan nhanh chóng và dễ hiểu về cách ca sử dụng hoạt động trong hệ thống.

- Một mô tả rút gọn thường bao gồm:
	1. **Tên ca sử dụng**: Đề cập ngắn gọn đến chức năng hoặc mục tiêu của ca sử dụng (ví dụ: "Rút tiền").
	2. **Tác nhân liên quan**: Định rõ ai hoặc hệ thống nào sẽ tương tác với ca sử dụng (ví dụ: "Khách hàng").
	3. **Mục tiêu**: Mô tả mục tiêu chính mà ca sử dụng hướng đến (ví dụ: "Cho phép khách hàng rút tiền mặt từ tài khoản ngân hàng").
	4. Mô tả tổng quát: Mô tả ngắn gọn các bước chính diễn ra trong ca sử dụng (không đi vào chi tiết kịch bản).
- Ví dụ về mô tả rút gọn:
	- **Tên ca sử dụng**: Rút tiền
	- **Tác nhân liên quan**: Khách hàng
	- **Mục tiêu**: Cung cấp tiền mặt từ tài khoản ngân hàng cho khách hàng
	- **Mô tả tổng quát**: Khách hàng đưa thẻ vào máy ATM, nhập mã PIN, chọn số tiền muốn rút và nhận tiền.

##### 7. Mô tả mở rộng ca sử dụng (expanded use case description) cần có những mục gì?
![[Pasted image 20250414230446.png]]
- **Mô tả mở rộng ca sử dụng (expanded use case description)** thường được trình bày chi tiết hơn so với mô tả rút gọn, giúp cung cấp đầy đủ thông tin cần thiết để hiểu rõ từng ca sử dụng. Dưới đây là các mục thường có trong mô tả này:
	1. **Tên ca sử dụng**: Tên rõ ràng, mô tả mục đích chính của ca sử dụng.
	2. **Tác nhân liên hệ**: Các tác nhân chính và phụ tương tác với ca sử dụng.
	3. **Mục tiêu (Goal)**: Mục tiêu mà ca sử dụng hướng đến, giúp xác định giá trị đem lại.
	4. **Mô tả tổng quan (Overview)**: Tóm tắt nhanh về ca sử dụng.
	5. **Tiền điều kiện (Pre-condition)**: Các điều kiện phải được thỏa mãn trước khi ca sử dụng bắt đầu.
	6. **Dòng sự kiện chính (Typical course of events)**: Mô tả từng bước chính trong luồng hoạt động của ca sử dụng.
	7. **Các dòng sự kiện phụ (Alternative courses)**: Các trường hợp ngoại lệ hoặc các luồng sự kiện khác ngoài dòng chính.
	8. **Hậu điều kiện (Post-condition)**: Kết quả hoặc trạng thái hệ thống sau khi ca sử dụng hoàn thành.
	9. **Tham khảo (Cross-reference)**: Liên kết hoặc tham chiếu đến các yêu cầu hệ thống, hoặc các ca sử dụng khác có liên quan.
- Ví dụ: **mô tả mở rộng ca sử dụng (expanded use case description)** cho hệ thống rút tiền tại máy ATM:
	1. **Tên ca sử dụng**: Rút tiền từ ATM
	2. **Tác nhân liên hệ**:
	    - Chính: Khách hàng
	    - Phụ: Ngân hàng (hệ thống xử lý giao dịch)
	3. **Mục tiêu**: Khách hàng có thể rút tiền mặt từ tài khoản ngân hàng qua máy ATM.
	4. **Mô tả tổng quan**: Khi khách hàng muốn rút tiền, họ sử dụng máy ATM để thực hiện giao dịch. Hệ thống kiểm tra số dư tài khoản và thực hiện giao dịch rút tiền.
	5. **Tiền điều kiện**:
	    - ATM phải hoạt động bình thường.
	    - Khách hàng phải có thẻ ATM hợp lệ và mã PIN.
	    - ATM còn đủ tiền mặt và giấy in hóa đơn.
	6. **Dòng sự kiện chính**:
	    - Khách hàng đưa thẻ vào máy ATM.
	    - Hệ thống yêu cầu nhập mã PIN.
	    - Khách hàng nhập mã PIN.
	    - Hệ thống xác nhận thông tin mã PIN.
	    - Hệ thống hiển thị tùy chọn và khách hàng chọn “Rút tiền”.
	    - Khách hàng nhập số tiền muốn rút.
	    - Hệ thống kiểm tra số dư tài khoản và xử lý giao dịch.
	    - Hệ thống trả tiền mặt và in hóa đơn (nếu yêu cầu).
	7. **Dòng sự kiện phụ**:
	    - Nếu mã PIN sai quá 3 lần, thẻ bị khóa và giao dịch hủy bỏ.
	    - Nếu số tiền muốn rút vượt quá số dư, hiển thị thông báo lỗi và yêu cầu nhập lại.
	    - Nếu máy ATM không đủ tiền mặt, giao dịch không thể hoàn thành
	8. **Hậu điều kiện**:
	    - Tiền được rút thành công.
	    - Tài khoản của khách hàng được cập nhật lại số dư.
	    - ATM trở lại trạng thái sẵn sàng cho giao dịch mới.


##### 8. Quan hệ giữa tác nhân và ca sử dụng?
- **Tác nhân là người hoặc hệ thống tương tác với ca sử dụng**:
    - Tác nhân có thể là con người (ví dụ: khách hàng, nhân viên) hoặc hệ thống khác (ví dụ: hệ thống ngân hàng).
    - Tác nhân thực hiện các hành động hoặc yêu cầu hệ thống thực hiện các chức năng.
        
- **Ca sử dụng mô tả chức năng mà tác nhân cần**:
    - Mỗi ca sử dụng thể hiện một nhiệm vụ hoặc mục tiêu mà tác nhân muốn đạt được thông qua hệ thống.
    - Ví dụ: Tác nhân "Khách hàng" có thể yêu cầu hệ thống thực hiện ca sử dụng "Rút tiền".
        
- **Quan hệ giao tiếp (Association)**:
    - Quan hệ giữa tác nhân và ca sử dụng thường được biểu diễn bằng đường thẳng hoặc mũi tên trong biểu đồ ca sử dụng.
    - Nó cho thấy tác nhân nào tương tác với ca sử dụng nào.
        
- **Tác nhân có thể liên kết với nhiều ca sử dụng**:
    - Một tác nhân có thể thực hiện nhiều nhiệm vụ khác nhau, dẫn đến việc liên kết với nhiều ca sử dụng.
    - Ví dụ: Tác nhân "Khách hàng" có thể liên kết với các ca sử dụng như "Rút tiền", "Gửi tiền", "Truy vấn thông tin tài khoản".
        
- **Ca sử dụng có thể liên kết với nhiều tác nhân**:
    - Một ca sử dụng có thể phục vụ nhiều tác nhân khác nhau.
    - Ví dụ: Ca sử dụng "Cập nhật giá vé" có thể được thực hiện bởi cả "Nhân viên bán vé" và "Hệ thống quản lý".

##### 9. Nêu các loại quan hệ giữa các ca sử dụng?
- **Quan hệ << include >>**:
    - Một ca sử dụng bao gồm chức năng của một ca sử dụng khác.
    - Được sử dụng để tái sử dụng chức năng chung giữa các ca sử dụng.
    - Ví dụ: Ca sử dụng "Rút tiền" có thể bao gồm "Xác minh tài khoản".
- **Quan hệ << extend >>**:
    - Một ca sử dụng mở rộng hành vi của một ca sử dụng khác.
    - Được kích hoạt có điều kiện hoặc tùy chọn.
    - Ví dụ: Ca sử dụng "Rút tiền" có thể được mở rộng với "In hóa đơn" nếu khách hàng yêu cầu.
- **Quan hệ tổng quát hóa (Generalization)**:
    - Một ca sử dụng con kế thừa hành vi của ca sử dụng cha.
    - Được sử dụng để mô hình hóa các ca sử dụng có chung hành vi nhưng có thêm các đặc điểm riêng.
    - Ví dụ: Ca sử dụng "Thanh toán trực tuyến" có thể là tổng quát hóa của "Thanh toán qua thẻ" và "Thanh toán qua ví điện tử".



### Bài tập

#### 1. Cool Cuts
- ***Kịch bản A***: 
	- Tác nhân: 
		- Annie (Khách hàng)
		- Jen (Thợ )
	- Ca sử dụng:
		- Đặt lịch hẹn làm tóc
			- Tác nhân Annie gọi điện để đặt lịch
			- Jen xử lý thông tin và lên lịch
	- Biểu đồ ![[Pasted image 20250414233919.png]]
- ***Kịch bản B:***
	- Tác nhân: 
		- Mike (Giám đốc)
		- Rud (Thợ mới)
	- Ca sử dụng:
		- Thêm nhân viên
			- Mike nhập thông tin của Rud vào hệ thống
		- Quản lý ngày nghỉ:
			- Mike cập nhật ngày nghỉ của Rud
	- Biểu đồ 
		- ![[Pasted image 20250414234250.png]]
	- 