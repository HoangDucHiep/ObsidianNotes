---
title: Priority Queue
tags:
  - DataStructures
---
### Priority Queue là gì?
- Là một cấu trúc danh sách (Tương tư Queue và Stack), nhưng mỗi phần tử của nó được gán với một Priority (Độ ưu tiên). 
- Trong PQ, phần của nào có độ ưu tiên cao hơn sẽ được phục vụ trước![[Introduction.webp]]
### Tạo PQ với [[Binary Heap 🙀]]
- Ví dụ với MaxPQ
##### Các thao tác
- GetMax: Trả về phần tử có độ ưu tiên cao nhất trong PQ
	- Trả về phần tử đầu tiên
	- Độ phức tạp: $O(1)$
- SiftUp: Đẩy phần tử lên trên tới khi đúng vị trí hợp lệ
	- So sánh phần tử thứ i với cha của nó, nếu phần tử cha nhỏ hơn phần tử i, đổi chỗ chúng cho nhau
	- Set i tới phần tử cha
	- Tiếp tục lặp đến khi phần tử cha đảm bảo không nhỏ hơn phần tử con![[Drawing 2024-10-12 11.59.44.excalidraw 1.svg]]
	- Độ phức tạp: $O(log(n))$, do luôn thao tác trên 1 nhánh của cây, và cây được đảm bảo cân bằng vì dùng [[Binary Heap 🙀]]
- SiftDown: Đẩy phần tử xuống dưới tới khi đúng vị trí hợp lệ![[Heap 1.svg]]
	- Độ phức tạp: $O(log(n))$, tương tự SiftUp
- Insert: Thêm phần tử mới vào PQ
	- Chỉ cần thêm phần tử mới và cuối danh sách
	- Sau đó gọi SiftUp để đẩy phần tử lên vị trí thích hợp
	- Độ phức tạp: $O(log(n))$ theo độ phức tạp của SiftUp
- ExtractMax: Trả về và xóa phần tử có độ ưu tiên cao nhất
	- Lấy phần tử đầu
	- Đổi chỗ phần tử đầu với phần tử cuối
	- Xóa phần tử cuối ( giảm size )
	- Dùng SiftDown với phần tử đầu để đẩy nó xuống vị trí thích hợp
	- Độ phức tạp: $O(log(n))$, theo độ phức tạp cua SiftDown
- ChangePriority: Thay đổi độ ưu tiên của phần tử
	- Thay đổi giá trị phần tử tại i
	- Gọi SiftUp và SiftDown để đưa phần tử đến đúng vị trí
	- Độ phức tạp: $O(log(n))$
- Remove: Xóa phần tử khỏi PQ
	- Đổi chỗ phần tử i với phần tử cuối
	- Xóa phần tử cuối (giảm size)
	- Gọi SiftDown cho phần tử i để đẩy nó xuống vị trí đúng
		>  ❗***<span style="color:rgb(255, 0, 0)">Lưu ý***</span>: ta không cần dùng SiftUp vì bản thân phần tử tại i hiên tại chính là phần tử cuối cùng (Và là phần tử nhỏ hơn phần tử tại i), nên nó không thể lớn hơn cha của i
	- Độ phức tạp: $O(log(n))$
### Implement Code
- [Implement with C# and Python](https://github.com/HoangDucHiep/Coursera---Data-Structures-and-Algorithms-Specialization/tree/main/Data_Structures/data_structure_implementations/priority_queue)

### Ứng dụng
- Các thuật toán về đồ thị: Prim, Dijikstra, ...
- ... (Add soon)