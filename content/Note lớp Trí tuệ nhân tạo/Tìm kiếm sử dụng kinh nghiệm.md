---
title: Tìm kiếm sử dụng kinh nghiệm
tags:
  - Algorithms
---
### Thuật toán leo đồi

##### **1. Giới Thiệu Chung**
- **Định nghĩa:** Thuật toán leo đồi là một thuật toán tìm kiếm cục bộ được sử dụng cho các bài toán tối ưu hóa. Nó tìm kiếm giải pháp tốt nhất bằng cách lặp đi lặp lại khám phá các giải pháp lân cận.
- **Mục tiêu:** Tìm điểm cao nhất (giá trị lớn nhất) hoặc giải pháp tốt nhất trong một không gian tìm kiếm nhất định.
- **Ví dụ kinh điển:** Bài toán người bán hàng (Traveling Salesman Problem), trong đó mục tiêu là giảm thiểu khoảng cách di chuyển.
- **Ưu điểm:** Đơn giản, dễ hiểu và dễ cài đặt. Hiệu quả khi không gian tìm kiếm tương đối "mượt".
- **Hạn chế:** Dễ bị mắc kẹt trong cực đại cục bộ, bình nguyên () và đường gờ (ridge).
![[Pasted image 20250224130238.png]]
##### **2. Nguyên Lý Hoạt Động**
Các bước hoạt động của thuật toán leo đồi:
- **Khởi tạo:** Bắt đầu với một giải pháp ban đầu ngẫu nhiên hoặc được xác định trước. Điểm bắt đầu ban đầu có thể ảnh hưởng đến việc tìm kiếm giải pháp tốt nhất.
- **Đánh giá:** Sử dụng **hàm mục tiêu** để đo lường chất lượng hoặc độ phù hợp của giải pháp hiện tại. Hàm mục tiêu đóng vai trò như một chiếc "la bàn", giúp thuật toán xác định hướng "lên dốc" tới các giải pháp tốt hơn. Hàm mục tiêu gán một điểm số hoặc giá trị cho mỗi giải pháp có thể, cho phép thuật toán hiểu được hướng nào dẫn đến các giải pháp tốt hơn .
- **Tạo láng giềng:** Tạo ra các giải pháp lân cận bằng cách thực hiện các thay đổi nhỏ đối với giải pháp hiện tại.
- **Chọn láng giềng tốt nhất:** Chọn giải pháp lân cận tốt nhất dựa trên giá trị hàm mục tiêu. Có nhiều cách để chọn các giải pháp lân cận, dẫn đến các loại thuật toán leo đồi khác nhau:
- **Leo đồi đơn giản:** Chọn trạng thái lân cận đầu tiên cải thiện chi phí hiện tại.
- **Leo đồi dốc nhất:** Kiểm tra tất cả các trạng thái lân cận và chọn trạng thái lân cận gần nhất với trạng thái mục tiêu.
- **Leo đồi ngẫu nhiên:** Chọn ngẫu nhiên một trạng thái lân cận và quyết định có chọn trạng thái đó hay không dựa trên việc nó có cải thiện trạng thái hiện tại hay không.
- **So sánh:** So sánh giá trị hàm mục tiêu của giải pháp lân cận tốt nhất với giải pháp hiện tại.
- **Lặp:** Lặp lại quá trình cho đến khi đạt được điều kiện dừng, chẳng hạn như đạt đến số lần lặp tối đa, đạt ngưỡng giá trị hàm mục tiêu hoặc hết thời gian.
- **Điều kiện dừng:** Thuật toán kết thúc khi không tìm thấy giải pháp lân cận nào tốt hơn giải pháp hiện tại.
##### **3. Các Loại Thuật Toán Leo Đồi**
- **Leo đồi đơn giản (Simple Hill Climbing):** Đánh giá các trạng thái lân cận từng cái một và chọn trạng thái đầu tiên cải thiện chi phí hiện tại. Nhanh chóng nhưng có thể bỏ lỡ các giải pháp tốt hơn.
- **Leo đồi dốc nhất (Steepest-Ascent Hill Climbing):** Kiểm tra tất cả các nút lân cận của trạng thái hiện tại và chọn nút lân cận gần nhất với trạng thái mục tiêu (cải thiện nhiều nhất). Tốn thời gian hơn nhưng thường tìm thấy các giải pháp tốt hơn.
- **Leo đồi ngẫu nhiên (Stochastic Hill Climbing):** Chọn ngẫu nhiên một nút lân cận và quyết định có chọn nút đó hay không dựa trên việc nó có cải thiện trạng thái hiện tại hay không.
##### **4. Các Vấn Đề Thường Gặp (Limitations) và Giải Pháp**
- **Cực đại cục bộ (Local Maximum):** Thuật toán bị mắc kẹt tại một trạng thái tốt hơn các trạng thái lân cận, nhưng không phải là trạng thái tốt nhất toàn cục.
- **Giải pháp:** Kỹ thuật backtracking, khởi động lại ngẫu nhiên (random restarts), ủ mô phỏng (simulated annealing).
- **Bình nguyên (Plateau):** Vùng phẳng trong không gian tìm kiếm, nơi tất cả các trạng thái lân cận có cùng giá trị.
- **Giải pháp:** Thực hiện các bước lớn hơn (random jumps) hoặc di chuyển theo các hướng khác nhau.
- **Đường gờ (Ridge):** Vùng cao hơn các khu vực xung quanh, nhưng có độ dốc và không thể đạt được trong một lần di chuyển.
- **Giải pháp:** Tìm kiếm hai chiều hoặc di chuyển theo các hướng khác nhau.
- **Sự phụ thuộc vào giải pháp ban đầu:** Chất lượng của giải pháp cuối cùng phụ thuộc nhiều vào giải pháp ban đầu được chọn.
##### **5. Ứng Dụng**
- **Trí tuệ nhân tạo:** Tối ưu hóa các tham số của mô hình học máy, tìm kiếm đường đi trong trò chơi.
- **Tối ưu hóa danh mục đầu tư:** Tìm sự phân bổ tài sản tối ưu để tối đa hóa lợi nhuận và giảm thiểu rủi ro.
- **Tối ưu hóa chuỗi cung ứng:** Tìm các tuyến đường giao hàng hiệu quả.
- **Lập lịch trình tài nguyên:** Tối ưu hóa lịch trình nhân viên hoặc sử dụng máy móc.
##### **6. Hàm Mục Tiêu (Objective Function) - Ví dụ Tối Ưu Hóa Danh Mục Đầu Tư**
- **Mục tiêu:** Cân bằng giữa lợi nhuận kỳ vọng và rủi ro danh mục đầu tư.
- **Đầu vào:** Tỷ lệ phần trăm đầu tư vào các loại tài sản khác nhau.
- **Các yếu tố:** Lợi nhuận kỳ vọng của từng tài sản.
- Độ biến động (rủi ro) của từng tài sản.
- Tổng tỷ lệ đầu tư phải bằng 100%.
- Không có tỷ lệ đầu tư âm (không bán khống).
- **Đầu ra:** Điểm số đánh giá chất lượng danh mục đầu tư (điểm càng cao càng tốt).