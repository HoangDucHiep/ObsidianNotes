---
title: Middleware
tags:
  - Full-Stack
---

> [!NOTE] Middleware là gì?
> - Middleware là **các hàm trung gian** được thực thi **giữa request của client và response của server**.
> - Chúng giúp xử lý, thay đổi, hoặc chặn request trước khi nó đến được route handler hoặc trước khi response được gửi lại.

- Middleware thường được sử dụng để:
	- **Xác thực (Authentication)**
	- **Ghi log (Logging)**
	- **Xử lý lỗi (Error handling)**
	- **CORS (Cross-Origin Resource Sharing)**
	- **Nén dữ liệu (Compression)**
	- **Chuyển đổi dữ liệu (Parsing)**
	- **Cache dữ liệu**