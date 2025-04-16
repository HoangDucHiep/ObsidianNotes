---
title: Authentication Scheme
tags:
  - ASPnetCore
---
> Authentication Scheme là tên hoặc định danh gán cho một phương thức xác thực cụ thể

### Liên tưởng
Bạn là **người quản lý sân bay** (ứng dụng ASP.NET Core).

- Bạn cài đặt **nhiều cổng kiểm tra** (scheme) để xử lý các loại hành khách (người dùng):
    1. **Cổng nội địa** - dùng Cookie để nhận diện người dùng thông thường.
    2. **Cổng quốc tế** - dùng JWT Token để xác thực người dùng API.
    3. **Cổng VIP** - dùng OAuth để xác thực qua Google hoặc Facebook.

Mỗi khi một hành khách đến sân bay:

1. Họ được dẫn đến đúng cổng dựa trên **loại vé** (scheme) của họ.
2. Nếu vé hợp lệ (authentication thành công), họ được phép vào (access granted).


``` c#
builder.Services.AddAuthentication(options =>
{
    options.DefaultAuthenticateScheme = "Cookies";  // Scheme mặc định
    options.DefaultChallengeScheme = "Google";     // Khi cần login, chuyển sang Google
})
.AddCookie("Cookies", options => // Cài đặt scheme Cookie
{
    options.LoginPath = "/Account/Login";
    options.AccessDeniedPath = "/Account/AccessDenied";
})
.AddJwtBearer("Bearer", options => // Cài đặt scheme JWT
{
    options.TokenValidationParameters = new TokenValidationParameters
    {
        ValidateIssuer = true,
        ValidateAudience = true,
        ValidIssuer = "yourdomain.com",
        ValidAudience = "yourdomain.com",
        IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes("YourSecretKey"))
    };
})
.AddGoogle("Google", options => // Cài đặt scheme OAuth (Google)
{
    options.ClientId = "YourGoogleClientId";
    options.ClientSecret = "YourGoogleClientSecret";
});
```
