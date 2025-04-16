### 1. Tổng Quan và Mục Tiêu

- **Mục đích của quy trình phát triển:**
    - Hiểu và phân tích nhu cầu của NSD (người sử dụng)
    - Xác định bài toán và thiết kế hệ thống
    - Xây dựng, chuyển giao, bảo trì và nâng cấp phần mềm
        
- **Hai khía cạnh quan trọng trong phát triển hệ thống:**
    - Quy trình: Các bước cần thực hiện từ khâu xác định đến chuyển giao   
    - Mô hình: Các phương tiện giúp diễn tả hệ thống (ví dụ: các biểu đồ UML, tài liệu mô tả)
        

---

### 2. Các Phương Pháp Phát Triển Phần Mềm
#### a. Phương pháp Thác Nước (Waterfall)

- **Ưu điểm:**
    - Các pha được xác định rõ ràng, hỗ trợ lên kế hoạch và phòng ngừa lỗi sớm
    - Có kết quả sau mỗi pha
        
- **Nhược điểm:**
    - Yêu cầu hoàn chỉnh tất cả các pha trước khi chuyển sang pha kế tiếp
    - Xử lý lỗi muộn và thời gian chuyển giao dài
        

#### b. Phát Triển Song Song (Parallel)

- **Ưu điểm:**
    - Thiết kế tổng thể giúp giảm thời gian phát triển
        
- **Nhược điểm:**
    - Khó khăn trong việc tích hợp các dự án con (subprojects) do phát triển đồng thời
        

#### c. Phát Triển Ứng Dụng Nhanh (RAD – Rapid Application Development)

- **Đặc điểm:**
    - Phù hợp khi yêu cầu của NSD không rõ ràng, dễ giao tiếp và nhanh chóng tạo ra bản mẫu (prototyping)
    - Thường đi kèm với các phương pháp Agile development
        
- **Ưu điểm:**
    - Giảm thời gian phát triển và tăng tính linh hoạt trong việc điều chỉnh yêu cầu
        

---

### 3. Cách Tiếp Cận Phát Triển Phần Mềm
#### a. Cách Tiếp Cận Truyền Thống

- Các bước phát triển được chia thành các pha riêng biệt:
    1. **Xác định nhu cầu:** Thu thập thông tin, phân tích các vấn đề của người dùng, xác định mục tiêu và phạm vi hệ thống
    2. **Phân tích:** Hình dung hệ thống “trong mắt” của NSD, liệt kê những chức năng cần thực hiện
    3. **Thiết kế:** Xác định cách hệ thống được xây dựng để đáp ứng yêu cầu
    4. **Cài đặt – Kiểm thử – Triển khai:** Quá trình chuyển hóa thiết kế thành phần mềm và đưa vào sử dụng
        

#### b. Cách Tiếp Cận Hướng Đối Tượng (Object-Oriented)

- Phát triển theo các vòng lặp (iterations) với mỗi vòng thực hiện các tiến trình cơ bản:
    - **Inception:** Khởi đầu dự án, nghiên cứu khả thi và xác định yêu cầu
    - **Elaboration:** Xác định kiến trúc hệ thống và thiết kế chi tiết
    - **Construction:** Xây dựng và lập trình hệ thống
    - **Transition:** Chuyển giao hệ thống cho khách hàng, hỗ trợ triển khai
        

---

### 4. Quá Trình RUP (Rational Unified Process)

- **RUP:** Một trong những phương pháp luận phát triển phần mềm hướng đối tượng, nhấn mạnh các pha lặp (iterations) và các tiến trình workflow:
    - Đưa ra lộ trình phát triển dựa trên các pha đã nêu ở phần Object-Oriented
    - Mỗi pha có các tiến trình cụ thể từ xác định yêu cầu đến thiết kế và hiện thực hóa
        

---

### 5. Yêu Cầu Hệ Thống và Nghiên Cứu Khả Thi
- **Yêu cầu hệ thống:**
    - Là tài liệu mô tả lý do xây dựng hệ thống và các giá trị mà hệ thống mang lại
    - Gồm các yếu tố như:
        - **Nhu cầu (Business Need):** Đối tượng khách hàng, mục đích, giải pháp tiềm năng
        - **Yêu cầu (Business Requirements):** Liệt kê các chức năng chính của hệ thống
        - **Lợi ích (Business Value):** Đo lường lợi ích kinh tế, như tăng doanh thu, giảm khiếu nại, …
            
- **Nghiên cứu khả thi:**
    - Xác định xem dự án có khả thi về mặt kỹ thuật, kinh tế và tổ chức hay không
    - Đánh giá rủi ro và tiềm năng thành công của dự án
        
---

### 6. Quản Lý Dự Án

- **Khái niệm dự án:**
    - Một tập hợp các hành động từ điểm khởi đầu đến điểm kết thúc nhằm tạo ra hệ thống có giá trị
        
- **Quy trình quản lý dự án:
    - **Lập kế hoạch:** Xác định các công việc (tasks), thời gian thực hiện, sự phụ thuộc giữa các công việc và phân công trách nhiệm
        
    - **Công cụ hỗ trợ:**
        - **Work Breakdown Structure (WBS):** Phân chia dự án thành các công việc nhỏ, rõ ràng
        - **Gantt Chart:** Biểu đồ thời gian thể hiện tiến độ và sự liên kết giữa các công việc

---

### 7. Timeboxing

- **Khái niệm Timeboxing:**
    - Quản lý dự án theo thời gian cố định với deadline không thay đổi
    - Chỉ tập trung vào các chức năng cốt lõi, loại bỏ các chức năng không cần thiết nếu không kịp thời gian
        
- **Các bước thực hiện Timeboxing:**
    1. Ấn định thời hạn hoàn thành dự án
    2. Xác định mức độ ưu tiên của các chức năng
    3. Xây dựng phần cốt lõi của hệ thống (các chức năng có độ ưu tiên cao nhất)
    4. Loại bỏ các chức năng không thể hoàn thành trong thời hạn đã định
    5. Bàn giao dự án với các chức năng cốt lõi
    6. Lặp lại các bước trên để hiệu chỉnh, nâng cấp hệ thống theo khung thời gian mới