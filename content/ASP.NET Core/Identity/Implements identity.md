---
title: Implements identity
tags:
  - ASPnetCore
---
### Install code scaffolder
`dotnet tool install dotnet-aspnet-codegenerator --version 8.0.* --global`

### Install packages
``` bash
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 8.0.*
dotnet add package Microsoft.AspNetCore.Identity.EntityFrameworkCore --version 8.0.*
dotnet add package Microsoft.AspNetCore.Identity.UI --version 8.0.*
dotnet add package Microsoft.EntityFrameworkCore.Design --version 8.0.*
dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 8.0.*
dotnet add package Microsoft.EntityFrameworkCore.Tools --version 8.0.*
```

### Scaffold to add default Identity components
``` bash
dotnet aspnet-codegenerator identity --useDefaultUI --dbContext RazorPagesPizzaAuth --userClass RazorPagesPizzaUser
```
In the preceding command:
- The generator identified as `identity` is used to add the Identity framework to the project.
- The `--useDefaultUI` option indicates that a Razor class library (RCL) containing the default UI elements is used. Bootstrap is used to style the components.
- The `--dbContext` option specifies the name of an EF Core database context class to generate.
- The `--userClass` option specifies the name of the user class to generate. The default user class is `IdentityUser`, but since the user class is extended in a later unit, a custom user class named `RazorPagesPizzaUser` is specified. The `RazorPagesPizzaUser` class is derived from `IdentityUser`.

- Scaffold đã tự thêm phần này vào Program.cs![[Pasted image 20250325125212.png]]

### Configure the database connection
- Thêm `ConnectionStrings` vào `appsettings.json`
``` json
"ConnectionStrings": {
    "RazorPagesPizzaAuthConnection": "Server=(localdb)\\mssqllocaldb;Database=RazorPagesPizza;Trusted_Connection=True;MultipleActiveResultSets=true"
}
```

### Update database
- Install EF core migration tool: 
``` bash
dotnet tool install dotnet-ef --version 8.0.* --global
```

- Tạo migration và update database
``` bash
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```


### Multifactor authentication
- Multifactor authentication (MFA) là một quá trình mà người dùng được nhắc về các hình thức nhận dạng bổ sung trong khi đăng nhập. Lời nhắc này có thể dành cho mã từ ứng dụng, giá trị mã thông báo phần cứng hoặc quét sinh trắc học. Khi bạn yêu cầu một loại xác thực thứ hai, bảo mật sẽ được tăng cường.
- Bằng chứng cần thiết để xác thực được phân loại thành ba loại:
	- Thứ mà ta biết, giống như password hay sercurity question
	- Thứ mà ta có, như hardware token hoặc một app trên điện thoại
	- Thứ mà là chúng ta, như vân tay hay khuôn mặt
#### Time-based one-time ppassword
- Time-based one-time password (TOTP) is a well-known algorithm that generates unique numerical codes that expire after 30 seconds. 
- The algorithm takes two inputs:
	- the current time
	- unique key.
- The user enters the key into a TOTP-compliant app when registering. Such apps include:
	- Microsoft Authenticator.
	- Google Authenticator.
	- _Many others!_
#### Thực hiện:
- Add QR code service:
``` bash
dotnet add package QRCoder --version 1.6.0
```
- Thêm service QRcode:
``` c#
using QRCoder;

namespace RazorPagesPizza.Services;
public class QRCodeService
{
    private readonly QRCodeGenerator _generator;

    public QRCodeService(QRCodeGenerator generator)
    {
        _generator = generator;
    }

    public string GetQRCodeAsBase64(string textToEncode)
    {
        QRCodeData qrCodeData = _generator.CreateQrCode(textToEncode, QRCodeGenerator.ECCLevel.Q);
        var qrCode = new PngByteQRCode(qrCodeData);

        return Convert.ToBase64String(qrCode.GetGraphic(4));
    }
}
```
- Đăng kí service trong Program.cs
``` c#
using Microsoft.AspNetCore.Identity;
using Microsoft.EntityFrameworkCore;
using RazorPagesPizza.Areas.Identity.Data;
using Microsoft.AspNetCore.Identity.UI.Services;
using RazorPagesPizza.Services;
using QRCoder;

var builder = WebApplication.CreateBuilder(args);
var connectionString = builder.Configuration.GetConnectionString("RazorPagesPizzaAuthConnection");
builder.Services.AddDbContext<RazorPagesPizzaAuth>(options => options.UseSqlServer(connectionString)); 
builder.Services.AddDefaultIdentity<RazorPagesPizzaUser>(options => options.SignIn.RequireConfirmedAccount = true)
      .AddEntityFrameworkStores<RazorPagesPizzaAuth>();

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.AddTransient<IEmailSender, EmailSender>();
builder.Services.AddSingleton(new QRCodeService(new QRCodeGenerator()));

var app = builder.Build();
```

- Tiếp: https://learn.microsoft.com/en-us/training/modules/secure-aspnet-core-identity/7-configure-multi-factor-authentication
### Authentication vs. authorization
- Authentication is a process in which a user is verified to be who they claim to be.
	Xác thực là một quá trình trong đó người dùng được xác minh là người mà họ tuyên bố là.

- Consider a sign-in form. When you enter your username in the form, you're claiming to be **you**. The form _authenticates_ you as the person you claim to be by verifying your password.
	Hãy xem xét một hình thức đăng nhập. Khi bạn nhập tên người dùng của mình trong biểu mẫu, bạn sẽ tự nhận là bạn. Biểu mẫu xác thực bạn là người mà bạn tuyên bố là bằng cách xác minh mật khẩu của bạn.

- _Authorization_ refers to the process that determines what an authenticated user is allowed to do. For example, an administration screen might be limited to users with a claim of `IsAdmin=True`. Since claims are associated with an identity, there can be no authorization without authentication.
	Ủy quyền đề cập đến quá trình xác định những gì người dùng được xác thực được phép làm. Ví dụ: màn hình quản trị có thể được giới hạn ở người dùng có yêu cầu isadmin = true. Vì các khiếu nại được liên kết với một danh tính, không thể có sự cho phép mà không có xác thực.

### Claims and policy-based authorization

- Claims are name-value pairs describing what the subject _is_, **not** what it can _do_! Claims are assigned by a trusted authority and are used to enforce authorization policies.
	Khiếu nại là các cặp giá trị tên mô tả đối tượng là gì, không phải những gì nó có thể làm! Yêu cầu được chỉ định bởi một cơ quan đáng tin cậy và được sử dụng để thực thi các chính sách ủy quyền.

- Consider a government-issued ID. The ID displays your attributes. These are claims. Interested parties can observe the ID, verify its source and authenticity, and make decisions based on the attributes. The decisions enforce a policy.
	Hãy xem xét giấy tờ tùy thân do chính phủ cấp. ID hiển thị các thuộc tính của bạn. Đây là những tuyên bố. Các bên quan tâm có thể quan sát ID, xác minh nguồn gốc và tính xác thực của nó, đồng thời đưa ra quyết định dựa trên các thuộc tính. Các quyết định thực thi một chính sách.

- Look to bars and taverns for a more concrete example. Alice wants to purchase an adult beverage. The bartender examines Alice's credentials and observes the claim of her birth date. They then enforce a policy based on that birth date, and Alice is authorized to purchase the drink.
	Nhìn vào các quán bar và quán rượu để biết một ví dụ cụ thể hơn. Alice muốn mua đồ uống dành cho người lớn. Người pha chế kiểm tra thông tin đăng nhập của Alice và quan sát tuyên bố về ngày sinh của cô. Sau đó, họ thực thi một chính sách dựa trên ngày sinh đó và Alice được phép mua đồ uống.
#### Thực hiện:
https://learn.microsoft.com/en-us/training/modules/secure-aspnet-core-identity/9-enable-claims-policy-authorization