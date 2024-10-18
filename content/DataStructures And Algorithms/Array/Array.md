---
title: Array
tags:
  - DataStructures
---
### Mảng là gì?

>***<mark style="background: #D2B3FFA6;">Mảng (Array)</mark>*** là một tập hợp các phần tử cùng kiểu và có kích thước cố định, được lưu trữ liên tiếp nhau trên bộ nhớ

### Đặc điểm của mảng
- Vị trí của một phần tử trong mảng có thể tìm bằng cách $array\_address + elem\_size x (i - first\_index)$
- Thời gian của các operation cơ bản

	|     | Add    | Remove    | Access |
	| --- | --- | --- | --- |
	|Beginning     | O(n)    | O(n)    | O(1) |
	|End     | O(1)    | O(1)    | O(1) |
	|Middel     | O(n)    | O(n)    | O(1) |
	Vậy array có thời gian truy cập ***hằng số (constant)***, và thời gian thêm bớt worst case là ***tuyến tính (linear)***
	