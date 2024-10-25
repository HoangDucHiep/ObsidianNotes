## <span style="color:rgb(133, 255, 135)">Product</span>

- `ProductID` - PK
- `VendorID` - FK
- `CategoryID` - FK
- `Name` - NOT NULL
- `Slug` - NOT NULL
- `Description` - NULL
- `Price` - NULL
- `Stock` - NULL
- `SKU` - NULL
- `HasVariant` - NOT NULL (default false)
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## <span style="color:rgb(133, 255, 135)">Category<span style="color:rgb(133, 255, 135)">
</span></span>
- `CategoryID` - PK
- `ParentCategory` - FK
- `Name` - NOT NULL
- `Slug` - NOT NULL
- `Description` - NULL
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## <span style="color:rgb(133, 255, 135)">Vendor</span>

- `VendorID` - PK
- `Name` - NOT NULL
- `Email` - NOT NULL
- `Phone` - NULL
- `Address` - NULL
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## <span style="color:rgb(133, 255, 135)">ProductVariant</span>

- `VariantID` - PK
- `ProductID` - FK
- `Name` - NOT NULL
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## <span style="color:rgb(133, 255, 135)">ProductVariantOption</span>

- `OptionID` - PK
- `VariantID` - FK
- `Value` - NOT NULL
- `Price` - NOT NULL
- `Stock` - NOT NULL
- `SKU` - NOT NULL
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## Order

- `OrderID` - PK
- `CustomerID` - FK
- `Status` - NOT NULL
- `TotalAmount` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## OrderDetail

- `OrderDetailID` - PK
- `OrderID` - FK
- `ProductVariantOptionID` - FK
- `Quantity` - NOT NULL
- `Price` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## ProductImage

- `ImageID` - PK
- `ProductID` - FK
- `URL` - NOT NULL
- `IsPrimary` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## ProductReview

- `ReviewID` - PK
- `ProductID` - FK
- `CustomerID` - FK
- `Rating` - NOT NULL
- `Comment` - NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## InventoryHistory

- `HistoryID` - PK
- `ProductVariantOptionID` - FK
- `Type` - NOT NULL
- `Quantity` - NOT NULL
- `Note` - NULL
- `CreatedAt` - NOT NULL

### Notes

1. Khi `HasVariant = false`:
    - `Product.Price`, `Stock`, `SKU` phải có giá trị
    - Không có dữ liệu tại `ProductVariant`
2. Khi `HasVariant = true`:
    - `Product.Price`, `Stock`, `SKU` phải là NULL
    - Phải có dữ liệu tại `ProductVariant` và `ProductVariantOption`

### Ví dụ về SKU
- Product không có variant: `AT001` (Basic T-shirt)
- Product có variant: `APL-DEN-S` (Black Polo Shirt size S)

## User

- `UserID` - PK
- `Email` - NOT NULL UNIQUE
- `Password` - NOT NULL
- `Phone` - NULL
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## UserRole

- `RoleID` - PK
- `Name` - NOT NULL (ADMIN, CUSTOMER, VENDOR)
- `Description` - NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## UserRoleMapping

- `UserID` - PK, FK
- `RoleID` - PK, FK
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## Customer (User profile khi là khách hàng)

- `CustomerID` - PK
- `UserID` - FK UNIQUE
- `FirstName` - NOT NULL
- `LastName` - NOT NULL
- `Address` - NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## Vendor (User profile khi là người bán)

- `VendorID` - PK
- `UserID` - FK UNIQUE
- `BusinessName` - NOT NULL
- `BusinessAddress` - NOT NULL
- `BusinessPhone` - NOT NULL
- `TaxCode` - NULL
- `Status` - NOT NULL (PENDING, ACTIVE, REJECTED, BANNED)
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

### Notes

1. Khi user đăng ký:
    - Tạo record trong `User`
    - Tạo record trong `UserRoleMapping` với role CUSTOMER
    - Tạo record trong `Customer`
2. Khi user đăng ký làm người bán:
    - Tạo record trong `Vendor` với status PENDING
    - Admin duyệt -> update `Vendor.Status = ACTIVE`
    - Tạo thêm record trong `UserRoleMapping` với role VENDOR
3. Admin:
    - Là record trong `User` được map với role ADMIN
    - Có quyền cao nhất trong hệ thống
    - Có thể quản lý tất cả các đối tượng khác
4. Trong bảng `Order`:
    - Đổi `CustomerID` FK reference tới bảng `Customer` thay vì `User`
5. Trong bảng `ProductReview`:
    - Đổi `CustomerID` FK reference tới bảng `Customer` thay vì `User`