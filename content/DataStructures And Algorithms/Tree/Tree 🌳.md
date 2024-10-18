---
title: Tree 🌳
tags:
  - DataStructures
---
#### Tree là gì
> - Tree là một cấu trúc dữ liệu lưu trữ dữ liệu theo thứ bậc (hierarchically) thay vì tuyến tính (linear) - chẳng hạn như [[Linked List]]
> - Tree là
> 	- rỗng
> 	- hoặc là node, trong đó mỗi node chứa giá trị (key), và các cây con

- Ví dụ:
	
#### Một số thuật ngữ
- ***<span style="color:rgb(135, 70, 200)">Root***:</span> Là node gốc, node trên cùng (Là node 'Fred' ở ví dụ trên)
- ***<span style="color:rgb(135, 70, 200)">Child*** </span>là con trực tiếp của một Parent:
	- Kate là parent của Sam và Hugh
	- Sam và Hugh là child (children  :>) của Kate
- <span style="color:rgb(135, 70, 200)">***Ancestors***</span>: parent, parent của parent, ...
	- Fred và Kate là Ancestor của Sam
- <span style="color:rgb(135, 70, 200)">***Decendants***</span>: Con cháu chút chít, ....
	- Kate, Sally, Jim, Sam, Hugh đều là Decendants của Fred
- <span style="color:rgb(135, 70, 200)">***Sibling***</span>: Các node có cùng Parent
	- Kate, Sally, Jim là Sibling
- <span style="color:rgb(135, 70, 200)">***Leaf***</span>: Node không có children
	- Sam, Hugh, Sally, Jim
- <span style="color:rgb(135, 70, 200)">***Interior node***</span>: non-leaf - không phải là leaf
	- Kate, Fred
- <span style="color:rgb(135, 70, 200)">***Level***</span>: 1+ số cạnh giữa root và node
	- Level 1: Fred
	- Level 2: Kate, Sally, Jim
	- Level 3: Sam, Hugh
- <span style="color:rgb(135, 70, 200)">***Height***</span>: chiều cao của cây, là độ sâu lớn nhất từ node tới leaf sâu nhất của nó
	- Height 1: Sam, Hugh, Sally, Jim
	- Height 2: Kate
	- Height 3: Fred
- <span style="color:rgb(135, 70, 200)">***Forest***</span>: Tập hợp nhiều tree

#### Tạo tree 🌱
> [Source code C# và Python](https://github.com/HoangDucHiep/Coursera---Data-Structures-and-Algorithms-Specialization/tree/main/Data_Structures/data_structure_implementations/tree)
