---
title: Entity Framework Core
tags:
  - ASPnetCore
  - EF-Core
---
### Entity Framework Core (EF Core)
- Entity Framework Core là một [[Object Relational Mapper]] cho phép ưu trữ và truy xuất object từ nguồn dữ liệu

### Cài đặt
- To use EF Core with a SQL Server database, run the following dotnet CLI command: `dotnet add package Microsoft.EntityFrameworkCore.SqlServer`
- To add support for an InMemory data source, for testing: dotnet add package `Microsoft.EntityFrameworkCore.InMemory`

### DbContext
- `DbContext` là **lớp trung gian** giúp tương tác với database.
``` csharp
public class CatalogContext : DbContext 
{ 
	public CatalogContext(DbContextOptions options) : base(options) 
	{ } 
	public DbSet<CatalogItem> CatalogItems { get; set; } 
	public DbSet<CatalogBrand> CatalogBrands { get; set; } 
	public DbSet<CatalogType> CatalogTypes { get; set; } 
}
```
- `DbSet<CatalogItem>` giúp ánh xạ bảng CatalogItem trong database với class CatalogItem

### Configure EF Core
- EF Core dùng `DbContextOptionsBuilder` để config
``` csharp
// use SQL
builder.Services.AddDbContext<CatalogContext>( 
	options => options.UseSqlServer(
		builder.Configuration.GetConnectionString("DefaultConnection")));
// use in-memory database
builder.Services.AddDbContext<CatalogContext>(options =>
	options.UseInMemoryDatabase)
```

### Fetching and Storing data
- Ta sử dụng [[LINQ]] để retrieve và filter data bằng EF Core.
``` csharp
var brandItems = await _context.CatalogBrands
	.Where(b => b.Enabled)
	.OrderBy(b => b.Name)
	.Select(b => new SelectListItem { 
		Value = b.Id, Text = b.Name }) // will return IQueryable if stop at here
	.ToListAsync();
```
- Với add, EF Core track changes với các entity mà nó fetch. Để lưu những thay đổi, ta sử dụng method `SaveChangeAsync` của `DbContext`.
``` csharp
// create 
var newBrand = new CatalogBrand() { Brand = "Acme" }; 
_context.Add(newBrand); 
await _context.SaveChangesAsync(); 

// read and update 
var existingBrand = _context.CatalogBrands.Find(1); 
existingBrand.Brand = "Updated Brand"; 
await _context.SaveChangesAsync(); 

// read and delete (alternate Find syntax) 
var brandToDelete = _context.Find(2); 
_context.CatalogBrands.Remove(brandToDelete); 
await _context.SaveChangesAsync();
```

### Fetching related data
- Khi EF Core retrieve dữ liệu, nó chỉ lấy các dữ liệu trực tiếp với các entity đó, chứ không kèm theo các dữ liệu về navigation quan hệ. Điều đó để tránh populate quá nhiều dữ liệu không cần thiết, giúp tiếp kiệm thời gian.
- Để chứa cả các dữ liệu navigation đó, ta dùng [[Eager loading & Lazy loading | eager loading]]
``` csharp
// .Include requires using Microsoft.EntityFrameworkCore 
var brandsWithItems = await _context.CatalogBrands
	.Include(b => b.Items)
	//.Include("Items.Products") get even more deep
	.ToListAsync();
```

### Encapsulating data
``` csharp
public class Basket : BaseEntity 
{ 
	public string BuyerId { get; set; } 
	private readonly List _items = new List(); 
	public IReadOnlyCollection Items => _items.AsReadOnly(); 
	
	public void AddItem(int catalogItemId, decimal unitPrice, int quantity = 1) 
	{ 
		var existingItem = Items.FirstOrDefault(i => i.CatalogItemId == catalogItemId); 
		if (existingItem == null) 
		{ 
			_items.Add(new BasketItem() 
			{ 
				CatalogItemId = catalogItemId, 
				Quantity = quantity, 
				UnitPrice = unitPrice 
			});
		} else existingItem.Quantity += quantity;
	} 
}
```
- Ở ví dụ này, thay vì exposes List thì ra exposes một IReadOnlyCollection.

### [Resilient-connections](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/work-with-data-in-asp-net-core-apps#resilient-connections)
