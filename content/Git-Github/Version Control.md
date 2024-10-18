---
title: Version Control
tags:
  - Git
---
> ***<span style="color:rgb(135, 70, 200)">Version Control</span>*** là hệ thống ghi lại các thay đổi của file hoặc các file theo thời gian và ta có thể quay trở lại các phiên bản đó khi cần

### Local Version Control Systems
- Theo dõi các các một các local trên máy tính![[Pasted image 20241017232034.png]]
- Tương tự với việc copy lại các file sang một thư mục khác
- Nhưng vì chỉ tồn tại một các nội bộ, nên nếu lỡ xóa mất những phiên bản copy đó, ta không thể lấy lại nữa :<
- Khó khăn để collab với người khác 
### Centralized Version Control Systems
- Hệ thống có một server duy nhất để quản lí các phiên bản tại đó, các người dùng sẽ thao tác qua chung một server đó![[Screenshot 2024-10-17 150902.png]]
- Với hệ thống này, nếu server mà cút, thì cũng không ai có thể dùng được nữa 😒

### Distributed Version Control Systems
- Với hệ thống này, mỗi clients không chỉ checkout phiên bản mới nhất, mà chứa toàn bộ repository, tất cả lịch sử các phiên bản.
- Do đó, nếu một server dies, và hệ thống được collab thông qua server đó,<span style="color:rgb(135, 70, 200)"> </span> bất kì clients nào cũng có thể backup trở lại server để khôi phục nó![[Pasted image 20241017232059.png]]