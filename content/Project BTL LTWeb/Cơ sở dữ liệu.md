## Product

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

## Category

- `CategoryID` - PK
- `ParentCategory` - FK
- `Name` - NOT NULL
- `Slug` - NOT NULL
- `Description` - NULL
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## Vendor

- `VendorID` - PK
- `Name` - NOT NULL
- `Email` - NOT NULL
- `Phone` - NULL
- `Address` - NULL
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## ProductVariant

- `VariantID` - PK
- `ProductID` - FK
- `Name` - NOT NULL
- `Status` - NOT NULL
- `CreatedAt` - NOT NULL
- `UpdatedAt` - NOT NULL

## ProductVariantOption

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