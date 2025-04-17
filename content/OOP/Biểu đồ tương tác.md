#### 1. Trình bày về hai loại biểu đồ tương tác: tên gọi, tác dụng, cách xây dựng, các ký hiệu và đặc điểm chính?
##### 1. **Biểu đồ trình tự (Sequence Diagram)**
- **Tên gọi**: Biểu đồ trình tự.
- **Tác dụng**:
    - Mô hình hóa luồng logic trong hệ thống một cách trực quan.
    - Hiển thị thứ tự thời gian của các thông điệp được gửi giữa các đối tượng.
    - Hỗ trợ phân tích và thiết kế hệ thống, đặc biệt trong việc mô hình hóa động (dynamic modeling).
- **Cách xây dựng**:
    1. Xác định ngữ cảnh (thường là một kịch bản trong ca sử dụng).
    2. Nhận diện các tác nhân và đối tượng tham gia.
    3. Thiết lập đường sống (lifeline) cho từng đối tượng.
    4. Thêm các thông điệp tương tác giữa các đối tượng.
    5. Có thể xác định các kích hoạt (activation) cho các đối tượng.
- **Các ký hiệu**:
    - Đường sống (Lifeline): Đại diện cho sự tồn tại của đối tượng trong một khoảng thời gian.
    - Thông điệp (Message): Mũi tên biểu diễn thông điệp được gửi giữa các đối tượng.
    - Kích hoạt (Activation): Thanh chữ nhật biểu diễn thời gian đối tượng thực hiện một hành động.
- **Đặc điểm chính**:
    - Tập trung vào thứ tự thời gian của các thông điệp.
    - Là một trong những biểu đồ phổ biến nhất trong UML.
        
##### 2. **Biểu đồ cộng tác (Collaboration Diagram)**
- **Tên gọi**: Biểu đồ cộng tác (hoặc Biểu đồ giao tiếp trong UML 2.0).
- **Tác dụng**:
    - Nhấn mạnh mối quan hệ cấu trúc giữa các đối tượng trong hệ thống.
    - Hiển thị cách các đối tượng kết nối và giao tiếp để thực hiện các nhiệm vụ.
    - Dễ dàng sửa đổi khi thiết kế trên giấy hoặc bảng.
- **Cách xây dựng**:
    1. Xác định ngữ cảnh.
    2. Nhận diện các tác nhân và đối tượng tham gia.
    3. Thêm các thông điệp giữa các đối tượng.
- **Các ký hiệu**:
    - Đối tượng (Object): Đại diện cho các thực thể tham gia vào tương tác.
    - Thông điệp (Message): Đường nối giữa các đối tượng biểu diễn thông điệp được gửi.
- **Đặc điểm chính**:
    - Tập trung vào mối quan hệ giữa các đối tượng hơn là thứ tự thời gian.
    - Thường được sử dụng để bổ sung cho biểu đồ trình tự.
#### 2. Sự khác nhau giữa biểu đồ trình tự và biểu đồ cộng tác?
##### 1. **Biểu đồ trình tự (Sequence Diagram)**
- **Tập trung vào**: Thứ tự thời gian của các thông điệp được gửi giữa các đối tượng.
- **Cách biểu diễn**:
    - Các đối tượng được sắp xếp theo chiều ngang.
    - Trục dọc biểu diễn thời gian, với các thông điệp được gửi từ trên xuống dưới.
    - Sử dụng đường sống (lifeline) và các mũi tên để biểu diễn thông điệp.
- **Đặc điểm chính**:
    - Dễ dàng theo dõi luồng thời gian của các tương tác.
    - Thích hợp để mô hình hóa các kịch bản cụ thể trong hệ thống.
- **Ưu điểm**:
    - Hiển thị rõ ràng thứ tự thực hiện các thông điệp.
    - Phù hợp để phân tích luồng công việc hoặc hành vi động.

##### 2. **Biểu đồ cộng tác (Collaboration Diagram)
- **Tập trung vào**: Mối quan hệ cấu trúc giữa các đối tượng trong hệ thống.
- **Cách biểu diễn**:
    - Các đối tượng được sắp xếp tự do trong không gian biểu đồ.
    - Các thông điệp được biểu diễn bằng các đường nối giữa các đối tượng, thường được đánh số để chỉ thứ tự.
        
- **Đặc điểm chính**:
    - Nhấn mạnh vai trò của các đối tượng trong tương tác.
    - Không có trục thời gian rõ ràng như biểu đồ trình tự.
- **Ưu điểm**:
    - Dễ dàng sửa đổi khi thiết kế trên giấy hoặc bảng.
    - Phù hợp để bổ sung cho biểu đồ trình tự.
#### 3. Nêu mối quan hệ giữa một kịch bản và biểu đồ hành động tương ứng nó?
Mối quan hệ giữa một kịch bản (scenario) và biểu đồ hành động (activity diagram) tương ứng là rất chặt chẽ, vì biểu đồ hành động được sử dụng để mô hình hóa luồng công việc hoặc các bước thực hiện của kịch bản đó. Dưới đây là các điểm chính:
1. **Biểu diễn trực quan**:
    - Biểu đồ hành động cung cấp một cách trực quan để mô tả các bước trong kịch bản, giúp dễ dàng hiểu được luồng công việc hoặc quy trình.
        
2. **Mô hình hóa luồng công việc**:
    - Kịch bản thường mô tả một chuỗi các hành động hoặc sự kiện. Biểu đồ hành động chuyển đổi các mô tả này thành một mô hình đồ họa, với các nút đại diện cho hành động và các mũi tên biểu diễn luồng giữa chúng.
        
3. **Xác định các điểm quyết định**:
    - Trong kịch bản, có thể có các điểm quyết định hoặc điều kiện. Biểu đồ hành động thể hiện rõ ràng các điểm này bằng cách sử dụng các ký hiệu như hình thoi (decision node).
        
4. **Hỗ trợ phân tích và thiết kế**:
    - Biểu đồ hành động giúp phân tích kịch bản để xác định các bước cần thiết và các đối tượng liên quan, từ đó hỗ trợ thiết kế hệ thống.
        
5. **Tài liệu hóa quy trình**:
    - Biểu đồ hành động là một công cụ tài liệu hóa hiệu quả, giúp ghi lại các kịch bản và quy trình để tham khảo trong tương lai.