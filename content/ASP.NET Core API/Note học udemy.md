- Sử dụng các DTO, một object chứa một số (cần thiết) hoặc tất cả các thuộc tính của object gốc, giúp API chỉ cần trả về lượng dữ liệu cần thiết, tăng hiệu quả
- Auto Mapper: Tự động map các thuộc tính của 2 object với nhau
- Seed data trong Db Context:![[Pasted image 20250106235327.png]]

- Validation
	- Thay vì : ![[Pasted image 20250109222903.png]]
	- Ta có thể tạo 1 class Attribute: ![[Pasted image 20250109222943.png]]
	 và dùng như sau:![[Pasted image 20250109223011.png]]
- Filter: Sử dụng Where, Contains:![[Pasted image 20250114225017.png]]
- Sorting: Sử dụng OrderBy ![[Pasted image 20250114225118.png]]

> [!Query theo property từ string input]
>  Sử dụng `EF.Property<string>(c, str)`
>  Với <span style="color:rgb(184, 123, 234)">c</span> là Model cần query, <span style="color:rgb(184, 123, 234)">str</span> là tên của property
> 
- Paging: Sử dụng Skip() để skip số lượng item và Take() để chọn số lượng Item ![[Pasted image 20250114225541.png]]


### Auth với [[JWT (JSON Web Token)]]

- Install các package:
```
Microsoft.AspNetCore.Authentication.JwtBearer
Microsoft.IdentityModel.Tokens
System.IdentityModel.Tokens.Jwt
Microsoft.AspNetCore.Identity.EntityFrameworkCore
```
- Tạo Auth db context và seed data
``` c#
public class NZWalkAuthDbContext : IdentityDbContext
{
    public NZWalkAuthDbContext(DbContextOptions<NZWalkAuthDbContext> options) : base(options)
    {

    }

    protected override void OnModelCreating(ModelBuilder builder)
    {
        base.OnModelCreating(builder);
        var readerRoleId = "cf3d5a6a-a835-4e0d-84ff-e28ff0895048";
        var writerRoleId = "6399765a-0a00-4826-bf38-c7ff78ad3b73";

        var roles = new List<IdentityRole>
        {
            new IdentityRole
            {
                Id = readerRoleId,
                ConcurrencyStamp = readerRoleId,
                Name = "Reader",
                NormalizedName = "Reader".ToUpper()
            },
            new IdentityRole
            {
                Id = writerRoleId,
                ConcurrencyStamp = readerRoleId,
                Name = "Writer",
                NormalizedName = "Writer".ToUpper()
            }
        };
        builder.Entity<IdentityRole>().HasData(roles);
    }
}
```
- Tạo thêm Connection string cho auth db context
``` json
"ConnectionStrings": {
    "DefaultConnectionString": "Server=HOANGHIEP\\DEV;Database=NZWalkDb;Trusted_Connection=True;TrustServerCertificate=True;",

    "DefaultAuthConnectionString": "Server=HOANGHIEP\\DEV;Database=NZWalkAuthDb;Trusted_Connection=True;TrustServerCertificate=True;"
  },
```

- Config jwt và Inject auth db context:
``` c#
builder.Services.AddDbContext<NZWalkDbContext>(options =>
  options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnectionString")));

builder.Services.AddDbContext<NZWalkAuthDbContext>(option => option.UseSqlServer(builder.Configuration.GetConnectionString("DefaultAuthConnectionString")));

builder.Services.AddScoped<IRegionRepository, SQLRegionRepository>();
builder.Services.AddScoped<IWalkRepository, SQLWalkRepository>();
builder.Services.AddAutoMapper(typeof(AutoMapperProfiles));


builder.Services.AddIdentityCore<IdentityUser>()
    .AddRoles<IdentityRole>()
    .AddTokenProvider<DataProtectorTokenProvider<IdentityUser>>("NZWalk")
    .AddEntityFrameworkStores<NZWalkAuthDbContext>()
    .AddDefaultTokenProviders();

builder.Services.Configure<IdentityOptions>(options =>
    {
        options.Password.RequireDigit = false;
        options.Password.RequireLowercase = false;
        options.Password.RequireNonAlphanumeric = false;
        options.Password.RequireUppercase = false;
        options.Password.RequiredLength = 6;
        options.Password.RequiredUniqueChars = 1;
    });

builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(o =>
    {
        o.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            ValidIssuer = builder.Configuration["Jwt:Issuer"],
            ValidAudience = builder.Configuration["Jwt:Audience"],
            IssuerSigningKey = new SymmetricSecurityKey(
                Encoding.UTF8.GetBytes(builder.Configuration["Jwt:Key"])
            )
        };
    });
  
var app = builder.Build();
```

- Migration và Update database cần thêm --context
``` shell
dotnet ef migrations add "Creating Auth Database" --context "NZWalkAuthDbContext"
dotnet ef database update  --context "NZWalkAuthDbContext"
```
- Tạo auth controller
``` c#
public class AuthController : ControllerBase
{
    private readonly UserManager<IdentityUser> _userManager;

    public AuthController(UserManager<IdentityUser> userManager)
    {
        _userManager = userManager;

    }

    [HttpPost]
    [Route("Register")]
    public async Task<IActionResult> Register([FromBody] RegisterRequestDto registerRequestDto)
    {
        var identityUser = new IdentityUser
        {
            UserName = registerRequestDto.Username,
            Email = registerRequestDto.Username,
        };
		// create new user
        var identityResult = await _userManager.CreateAsync(identityUser, registerRequestDto.Password);
        if (identityResult.Succeeded)  // if create new user successfully
        {
            // Add roles to this
            if (registerRequestDto.Roles != null &&  registerRequestDto.Roles.Any())
            {
                identityResult = await _userManager.AddToRolesAsync(identityUser, registerRequestDto.Roles);
                if (identityResult.Succeeded)
                {
                    return Ok("User was registered! PLease login.");
                }
            }
        }

        return BadRequest("Something went wrong");
    }
}
```

#### Tạo action login với token
``` c#
[HttpPost]
[Route("Login")]
public async Task<IActionResult> Login([FromBody] LoginRequestDto loginRequestDto)
{
	var user = await _userManager.FindByEmailAsync(loginRequestDto.Username);  // GET THE USER WITH USERNAME
	if (user != null)     // IF HAVE USER WITH THAT USERNAME
    {
	    var checkPasswordResult = await _userManager.CheckPasswordAsync(user, loginRequestDto.Password);  // WE CHECK THE PASSWORD
        if (checkPasswordResult) {   // IF THE RIGHT PASSWORD
	        // create token
            var roles = await _userManager.GetRolesAsync(user);    // GET USER'S ROLES
            if (roles != null)
            {
	            var token = _tokenRepository.CreateJWTToken(user, roles.ToList());    // CREATE TOKEN
                LoginResponseDto response = new()
                {
	                JwtToken = token
                };
                return Ok(response);
            }
        }
    }
    return BadRequest("Username or password is incorrect");
}


/////////////////////////////////////////////////////////
// REPOSITORY
public class TokenRepository : ITokenRepository
{
    private readonly IConfiguration _configuration;
    
    public TokenRepository(IConfiguration configuration)
    {
        _configuration = configuration;
    }

    public string CreateJWTToken(IdentityUser user, List<string> roles)
    {
        // Create claims
        var claims = new List<Claim>();
        claims.Add(new Claim(ClaimTypes.Email, user.Email!));
        
        foreach (var role in roles)
        {
            claims.Add(new Claim(ClaimTypes.Role, role));
        }

        var key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(_configuration["Jwt:Key"]!));   // GET FROM appsettings.json
        var credentials = new SigningCredentials(key, SecurityAlgorithms.HmacSha256);
        var token = new JwtSecurityToken(_configuration["Jwt:Issuer"], _configuration["Jwt:Audience"], claims, DateTime.Now, DateTime.Now.AddMinutes(15), credentials);

        return new JwtSecurityTokenHandler().WriteToken(token);
    }
}


// appsetting.json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "DefaultConnectionString": "Server=HOANGHIEP\\DEV;Database=NZWalkDb;Trusted_Connection=True;TrustServerCertificate=True;",
    "DefaultAuthConnectionString": "Server=HOANGHIEP\\DEV;Database=NZWalkAuthDb;Trusted_Connection=True;TrustServerCertificate=True;"
  },
  "Jwt": {
    "Key": "bbuosyJSSGPOosflUSJ75JJHst6yjjjST5rt65SY77uhSYSko098HHhgst",
    "Issuer": "http://localhost:5136",
    "Audience": "http://localhost:5136"
  }
}
```

- Role based authorize
![[Pasted image 20250121001554.png]]



## Upload ảnh

#### Model
![[Pasted image 20250121234525.png]]

#### Controller
``` c#
[Route("api/[controller]")]
[ApiController]
public class ImagesController : ControllerBase
{
    private readonly IImageRepository _imageRepository;

    public ImagesController(IImageRepository repository)
    {
        _imageRepository = repository;
    }
    
    // POST: /api/images/upload
    [HttpPost]
    [Route("Upload")]
    public async Task<IActionResult> Upload([FromForm] ImageUploadRequestDto request)
    {
        ValidateFileUpload(request);
        if (ModelState.IsValid)
        {
            var imageDomainModel = new Image
            {
                File = request.File,
                FileExtention = Path.GetExtension(request.File.FileName),
                FileSizeInBytes = request.File.Length,
                FileName = request.FileName,
                FileDescription = request.FileDescription,
            };

            await _imageRepository.Upload(imageDomainModel);
            return Ok(imageDomainModel);
        }
        return BadRequest(ModelState);
    }

    private void ValidateFileUpload(ImageUploadRequestDto request)
    {
        var allowedExtensions = new string[] { ".jpg", ".jpeg", ".png" };
        if (!allowedExtensions.Contains(Path.GetExtension(request.File.FileName)))
        {
            ModelState.AddModelError("file", "Unsupported file extension");
        }
        if (request.File.Length > 10485760) // 10MB
        {
            ModelState.AddModelError("file", "File size must be less than 10MB, please upload a smaller file");
        }
    }
}
```

#### Repository
``` C#
public class LocalImageRepository : IImageRepository
{
    private readonly IWebHostEnvironment _webHostEnvironment;     // cần inject trong program.cs
    private readonly IHttpContextAccessor _httpContextAccessor;   // cần inject trong program.cs: builder.Services.AddHttpContextAccessor();
    private readonly NZWalkDbContext _dbContext;

    public LocalImageRepository(IWebHostEnvironment webHostEnvironment, IHttpContextAccessor httpContextAccessor, NZWalkDbContext dbContext)
    {
        _webHostEnvironment = webHostEnvironment;
        _httpContextAccessor = httpContextAccessor;
        _dbContext = dbContext;
    }
    
    public async Task<Image> Upload(Image image)
    {
        // create local path
        var localFilePath = Path.Combine(
            _webHostEnvironment.ContentRootPath,
            "Images",
            $"{image.FileName}{image.FileExtention}");
	    // upload
        using var stream = new FileStream(localFilePath, FileMode.Create);
        await image.File.CopyToAsync(stream);
        
        //
        var urlFilePath = $"{_httpContextAccessor.HttpContext.Request.Scheme}://{_httpContextAccessor.HttpContext.Request.Host}{_httpContextAccessor.HttpContext.Request.PathBase}/Images/{image.FileName}{image.FileExtention}";
        image.FilePath = urlFilePath;
        // save
        await _dbContext.Images.AddAsync(image);
        await _dbContext.SaveChangesAsync();

        return image;
    }

}
```

#### Để xem được ảnh qua request
![[Pasted image 20250121234935.png]]

### Logging
- Install packages
	`Serilog`
	`Serilog.AspNetCore`
	`Serilog.Sinks.Console`
	`Serilog.Sinks.File`
- Inject
``` c#
// Add logging
var logger = new LoggerConfiguration()
    .WriteTo.Console()
    .WriteTo.File("Logs/NzWalks_Log.txt", rollingInterval: RollingInterval.Minute)
    .MinimumLevel.Information()
    .CreateLogger();


builder.Logging.ClearProviders();
builder.Logging.AddSerilog(logger);
```
- Sử dụng ![[Pasted image 20250208231157.png]]

### Global exception
- Tạo Middleware tự động xử lý exception, tránh trùng lặp
- Add middleware class
``` c#
using System.Net;
namespace NZWalks.API.Middlewares;

public class ExceptionHandlerMiddleware
{
    private readonly ILogger<ExceptionHandlerMiddleware> _logger;
    private readonly RequestDelegate _next;
  
    public ExceptionHandlerMiddleware(
        ILogger<ExceptionHandlerMiddleware> logger,
        RequestDelegate next
    )
    {
        _logger = logger;
        _next = next;
    }
  
    public async Task InvokeAsync(HttpContext httpContext)
    {
        try
        {
            await _next(httpContext);
        }
        catch (Exception ex)
        {
            var errorId = Guid.NewGuid();
            // Log this exception
            _logger.LogError(ex, $"{errorId} : {ex.Message}");
            // Return A Custom Error Response
            httpContext.Response.StatusCode = (int)HttpStatusCode.InternalServerError;
            httpContext.Response.ContentType = "application/json";
  
            var error = new
            {
                Id = errorId,
                ErrorMessage = "Something went wrong! We are looking into resolving this."
            };
            await httpContext.Response.WriteAsJsonAsync(error);
        }
    }
}
```
- Add middleware vào pipeline ![[Pasted image 20250208231409.png]]
- Sử dụng ![[Pasted image 20250208231424.png]]

### Versioning
- Manage multiple versions
- Provide backward compatibility
- Maintaining Consistency for Consumers
### Techniques
- URL-based versioning
- Query parameter-based versioning
- Header-based versioning