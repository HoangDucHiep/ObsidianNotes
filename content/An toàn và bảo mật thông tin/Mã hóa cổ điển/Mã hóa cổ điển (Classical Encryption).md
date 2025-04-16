---
title: Mã hóa cổ điển (Classical Encryption)
tags:
  - Cryptography_and_sercurity
---
- Là phương pháp mã hóa đơn giản nhất
- Mã cổ điển là mã đối xứng
- Có 2 loại gồm 
	- Mã thay thế (Mã thế)
	- Mã hoán vị (Mã chuyển vị)


### Terms
- **Plaintext**: Văn bản gốc (nội dung thông điệp ban đầu trước khi mã hóa).
- **Ciphertext**: Văn bản mã hóa (nội dung sau khi đã được mã hóa).
- **Enciphering / Encryption**: Mã hóa (quá trình chuyển đổi từ văn bản gốc sang văn bản mã hóa).
- **Deciphering / Decryption**: Giải mã (quá trình khôi phục văn bản gốc từ văn bản mã hóa).
- **Cryptography**: Mật mã học (nghiên cứu về các phương pháp mã hóa thông tin).
- **Cryptographic System / Cipher**: Hệ thống mật mã / Mã hóa (các hệ thống hoặc phương pháp được sử dụng để mã hóa thông tin).
- **Cryptanalysis**: Phân tích mật mã (các kỹ thuật dùng để giải mã mà không cần biết chi tiết về cách mã hóa).
- **Breaking the code**: Phá mã (cách gọi đơn giản của việc phân tích mật mã trong đời thường).
- **Cryptology**: Mật mã học toàn diện (bao gồm cả mật mã học và phân tích mật mã).

### Mã thế
- Là phương pháp mà từng kí tự (nhóm kí tự) trong bản rõ (plain text) được thay thế bằng một kí tự (một nhóm kí tự) khác để tạo ra bản mã. Bên nhận chỉ cần thay thế ngược lại trên bản mã để có được bản rõ ban đầu

### Mã chuyển vị
- Là phương pháp mà các kí tự trong bản rõ vẫn được giữ nguyên, chúng chỉ được sắp xếp lại vị trí để tạo ra bản mã. Tức là các kí tự trong bản rõ hoàn toàn không bị thay đổi bằng kí tự khác mà chỉ đảo chỗ của chúng để tạo thành bản mã.

### Mã đối xứng
- Sử dụng cùng 1 khóa K cho việc mã hóa và giải mã
- Mã khóa chia sẻ

## Symmetric cipher model
- Gồm 5 phần:
	- Plaintext: original data
	- Encryption algorithm
	- Secret key
	- Ciphertext: output data
	- Decryption algorithm
![[Pasted image 20250315124111.png]]
-  2 yêu cầu của mã đối xứng:
	- ***Thuật toán mã hóa phải đủ mạnh***, không thể giải mã ciphertext hay khám phá ra key dù biết một số lượng ciphertext cùng với plaintext đi cùng nhau.
	- ***Key cần được bảo mật***, chỉ người gưuir và người nhận biết.


### Cryptography (Hệ mật mã)
- Các đặc trưng:
	- Kiểu các thao tác dùng để chuyển plaintext thành ciphertext:
		- Substitution
		- Transposition
	- Số khóa được sử dụng
		- Với 1 key, hệ thống gọi là symmetric, 
		- 2 keys - asymmetric
	- Cách mà plaintext được xử lý
		- Block: 
			- plaintext được chia thành các block có kích thước xác định (64 bit, 128 bit)
			- Xử lý thuật toán cho từng block
		- Stream cipher:
			- Xử lý từng đơn vị thông tin đầu vào (bit, byte)
			- Độ dài khóa = độ dài bản rõ
			- Bộ đệm 1 lần

### An toàn của một hệ mã:
- An toàn không điều kiện: không quan trọng máy tính mạnh như thế nào, mã hoá không thể bị bẻ vì bản mãkhông cung cấp đủ thông tin để xác định duy nhất bản rõ. 
- An toàn tính toán: 
	- giá để phá hệ mã vượt quá giá trị của thông tin
	- thời gian để bẻ mã vượt quá thời gian có ích của thông tin



## SUBSTITUTION TECHNIQUES

### Caesar Cipher
- Dịch mỗi chữ cái trong plaintext lên k bước trong bảng chữ cái
![[Pasted image 20250315131815.png]]
- Encryption algorithm: $C\ =\ E(k, p)\ =\ (p + k)\ mod\ 26$
- Decryption algorithm: $p\ =\ E(k, C)\ =\ (C - k)\ mod\ 26$

- Thám mã caesar: 
	- Chỉ có 26 khóa có thể
	- Có thể brute force thử tất cả các khóa


### Monoalphabetic Substitution Cipher
#### Cách hoạt động
Để mã hóa một thông điệp bằng monoalphabetic substitution cipher, bạn cần thực hiện các bước sau:
1. **Chọn một hoán vị của bảng chữ cái làm khóa**: Đây là bảng ánh xạ quy định mỗi chữ cái trong bảng chữ cái gốc sẽ được thay thế bằng chữ cái nào. Ví dụ:
    - A → D
    - B → E
    - C → F
    - ...
    - Z → C
2. **Thay thế từng chữ cái**: Đối với mỗi chữ cái trong văn bản gốc, thay thế nó bằng chữ cái tương ứng trong bảng ánh xạ.  
    Ví dụ: Với bảng ánh xạ trên, từ "HELLO" sẽ được mã hóa thành "KHOOR".

Để giải mã, bạn chỉ cần sử dụng ánh xạ ngược lại (ví dụ: D → A, E → B, v.v.) để khôi phục văn bản gốc.
#### Ví dụ cụ thể
Giả sử bảng ánh xạ là:
- A → D
- B → E
- C → F
- D → G
- E → H
- ...
- H → K
- L → O
- O → R
- ...

Khi mã hóa từ "HELLO":
- H → K
- E → H
- L → O
- L → O
- O → R

Kết quả: "HELLO" trở thành "KHOOR".
#### Ưu điểm

- **Đơn giản**: Dễ hiểu và dễ thực hiện, không yêu cầu công cụ phức tạp.
- **Nhanh chóng**: Có thể mã hóa và giải mã bằng tay với một bảng ánh xạ.

#### Nhược điểm
- **Dễ bị phá vỡ**: Hệ thống này không an toàn vì dễ bị tấn công bằng **phân tích tần suất**. Trong một ngôn ngữ (như tiếng Anh hoặc tiếng Việt), các chữ cái có tần suất xuất hiện đặc trưng (ví dụ: "E" thường xuất hiện nhiều nhất trong tiếng Anh). Trong văn bản mã hóa, chữ cái thay thế cho "E" cũng sẽ xuất hiện với tần suất cao, giúp kẻ tấn công suy ra ánh xạ ban đầu, đặc biệt nếu văn bản mã hóa đủ dài.


### Playfair Cipher
