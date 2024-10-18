### Index là gì? 
- **Index** lưu trữ một bản sao của một hoặc nhiều cột trong bảng theo cấu trúc, giúp tăng hiệu quả trong việc thực hiện các truy vấn thay vì phải scan từng record
- Ví dụ: nếu bạn tạo chỉ mục trên khóa chính rồi tìm kiếm một hàng dữ liệu dựa trên một trong các giá trị khóa chính thì trước tiên SQL Server sẽ tìm giá trị đó trong chỉ mục, sau đó sử dụng chỉ mục để nhanh chóng định vị toàn bộ hàng của dữ liệu. Nếu không có chỉ mục, việc quét bảng sẽ phải được thực hiện để xác định vị trí hàng, điều này có thể ảnh hưởng đáng kể đến hiệu suất.
### Hash index:
- Hash index được tạo nên bởi một mảng gồm N các pointer, và mỗi phần tử của mảng được gọi là một ***hash bucket***
- Hash index sử dụng hàm băm F(K, N) với K là key và N là số Buckets, hàm băm sẽ map key tới index thích hợp trong mảng băm
- Các bucket không lưu trữ key hay giá trị đã băm của key, mà lưu trữ pointer trỏ tới dữ liệu
### Hàm băm là gì
- Hàm băm là bất kì thuật toán nào có thể ánh xạ dữ liệu có độ dài tùy ý trở thành dữ liệu có độ dài nhất định một cách xác định (determistic).
- Ví dụ: 
	- Hàm băm sử dụng độ dài của chỗi:
	- Vậy: F("John") = 4, F("Ed")= 2. Khi đó nếu chúng ta khởi tạo một hash index có 5 buckets và sử dụng hàm băm này,  thì pointer trỏ tới "john" và "ed" sẽ được lưu trữ lần lượt tại buckets 4 và 2.![[Pasted image 20241010000807.jpg]]
### Tìm kiếm
- Do hàm băm lưu trữ các pointer không theo thức tự nhất định, nên việc sử dụng hash index chỉ phù hợp khi ta tìm kiếm một các chính xác (VD: where name = "John")
- Khi đó tốc độ tìm kiếm sẽ rất nhanh do tốc độ là: Thời gian tính toán của hàm băm + Lấy địa chỉ tại index băm = O(1)
- Hash index không thể tìm kiếm theo phạm vi, vd như <, >, in(), ...
#### Collision (Va chạm)
- Vẫn với ví dụ trên, nếu ta muốn lưu trữ "Bill" thì sao. F("Bill") sẽ là 4, và nó trùng với F("John).
- Việc 2 key có cùng một giá trị băm được gọi là Collision, và thường xuyên xảy ra với hash function.
- Một hàm băm càng có nhiều collisions thì nó sẽ càng là một hàm băm tệ vì nó sẽ ảnh hưởng tới tốc độ của quá trình đọc dữ liệu
- Collision có thể xảy ra khi số lượng buckets là quá nhỏ so với số lượng key
### SQL Server xử lí collision
- SQL server sử dụng Hekaton engine để xử lí collision, nó sử dụng chaining bằng linked list.
- ![[Pasted image 20241010001953.jpg]]
- Có nhiều Collision sẽ khiến hiệu suất giảm đi nhiều
