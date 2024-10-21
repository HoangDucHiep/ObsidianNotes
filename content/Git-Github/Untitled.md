- git add 
- git add .

- git commit -m ""
- git branch <name> as
- git branch -a: show all branch
	- fix nhiều dòng: `git config --global --replace-all core.pager "less -F -X"`
- git checkout <branch name>: chuyen sang branhc
- git checkout -b <branch name>: tạo branch mới và chuyển sang branch đó
![[Pasted image 20241020005753.png]]
- Merge feature vào main
	- checkout main
	- git merge feature -m ""
- View commit history
	- git log
	-  git log --oneline
	- git log --oneline --graph (<span style="color:rgb(255, 0, 0)">This shit is so good</span>)
- Xóa branch
	- git branch -d <name>
	- 