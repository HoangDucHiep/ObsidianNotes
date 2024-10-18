---
title: 3 Git States
tags:
  - Git
---
- Git có 3 state chính mà các file có thể được đặt: ***modified***, ***staged***, ***commited***
- <span style="color:rgb(112, 48, 160)">Modified</span> là trạng thái ta ***đã thay đổi*** một file nhưng ***chưa commit*** nó
- <span style="color:rgb(112, 48, 160)">Staged</span> là trạng thái mà ta đã đánh dấu nhưng file đã modified ở version hiện tại để được có trong sẽ được trong commit snapshot tiếp theo
- Commited là trạng thái dữ liệu đã được lưu vào [[Git Repository | Git Repository]]![[Pasted image 20241017230551.png]]
- Basic workflow:
	- Sửa đổi các file trong working tree
	- Add các files đã sử đổi vào staging area
	- Commit, lấy các files từ staging area, tạo snapshot và lưu trữ vĩnh viễn trong Git Directory