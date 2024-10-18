---
title: Git configuration
tags:
  - Git
---
### Git configuration levels
![[git-config-levels-removebg-preview.png]]
- System: Toàn bộ người dùng một máy tính
- Global: Toàn bộ các project của 1 người dùng
- Local: Trong 1 project

### Một số lệnh config
- Xem tất cả các settings của mình 
	``` bash
	$ git config --list --show-origin
	```

- Config identity
	- Set username và email
	``` shell
	$ git config --global user.name "John Doe"
	$ git config --global user.email johndoe@example.com
	```
- Set default branch name
	- Branch mặc định được git tạo có tên là ***master*** , ta có thể đổi tên của branch mặc định bằng lệnh
	``` bash
	$ git config --global init.defaultBranch main
	```