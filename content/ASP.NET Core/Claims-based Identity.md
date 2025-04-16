
> [!Definition] Title
> Trong ASP.NET Core, ClaimsPrincipal là object biểu diễn cho user
> 

- Một ClaimsPrincipal các ClaimsIdentity object cho từng [[Authentication Scheme]], và các ClaimsIdentity lại chứa các Claims![[Pasted image 20250110221007.png]]
- Claims là các cặp name value đại diện cho các thuộc tính của người dùng được xác thực. 
- Ví dụ: bạn có thể lưu trữ số nhân viên của người dùng dưới dạng yêu cầu. Yêu cầu sau đó có thể được sử dụng như một phần của authorization policies. Bạn có thể tạo một policy có tên là “EmployeeOnly” yêu cầu sự tồn tại của một claim gọi là "EmployeeNumber", như trong ví dụ này:
``` csharp
public void ConfigureServices(IServiceCollection services) 
{ 
	services.AddMvc(); 
	services.AddAuthorization(options => { options.AddPolicy("EmployeeOnly", policy => policy.RequireClaim("EmployeeNumber")); 
	}); 
}
```