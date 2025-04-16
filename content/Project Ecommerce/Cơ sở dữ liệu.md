## 1. Users, Roles & Phân Quyền

### **Users**
- id: INT (Primary Key)
- username: VARCHAR
- email: VARCHAR
- password_hash: VARCHAR
- first_name: VARCHAR
- last_name: VARCHAR
- phone_number
- status (active, inactive, banned)
- created_at: DATETIME
- updated_at: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### **Roles**

- **id**: INT (PK)
- **name**: VARCHAR  
    _(Các giá trị: "admin", "vendor", "customer")_

### **UserRoles**

- **user_id**: INT (FK → Users.id)
- **role_id**: INT (FK → Roles.id)  
- assigned_at
    _Primary Key: (user_id, role_id)_

---

## 2. Vendors & Categories

### **Vendors**

- id: INT (Primary Key)
- user_id: INT (Foreign Key → Users.id)
- store_name: VARCHAR
- business_registration_number: VARCHAR
- description: TEXT
- logo_url: VARCHAR
- rating: DECIMAL(3,2)
- created_at: DATETIME
- updated_at: DATETIME
- status: ("active", "pending approval", "suspended")
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### **Categories**

- **id**: INT (PK)
- **name**: VARCHAR
- description
- is_active
- **parent_id**: INT (Foreign Key → Categories.id, nullable)
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

---

## 3. Sản phẩm & Liên quan

### **Products**

- **id**: INT (PK)
- **vendor_id**: INT (FK → Vendors.id)
- **category_id**: INT (FK → Categories.id)
- **name**: VARCHAR
- **description**: TEXT
- **slug**: VARCHAR
- **base_price**: DECIMAL
- is_active: BOOLEAN
- created_at: DATETIME
- updated_at: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### **Images**

_Bảng dùng để lưu trữ media của cả sản phẩm và variant._

- **id**: INT (PK)
- **product_id**: INT (FK → Products.id, NOT NULL)
- **variant_id**: INT (FK → ProductVariants.id, NULLABLE)
    - Nếu là ảnh của sản phẩm thì **variant_id** là NULL
    - Nếu là ảnh của variant thì **variant_id** khác NULL
- **media_type**: VARCHAR
    - Cho product: "image" hoặc "video" (với ràng buộc chỉ tối đa 1 video)
    - Cho variant: chỉ "image" được phép
- **media_url**: VARCHAR
- **alt_text**: VARCHAR
- is_thumbnail
- **created_at**: DATETIME
- **updated_at**: DATETIME

_Lưu ý nghiệp vụ:_

- Với `variant_id` khác NULL, chỉ chấp nhận `media_type` = "image".
- Với sản phẩm, chỉ cho phép tối đa 1 bản ghi có `media_type` = "video" (xử lý qua logic ứng dụng hoặc unique constraint nếu DB hỗ trợ).

### **ProductVariants**

- **id**: INT (PK)
- **product_id**: INT (FK → Products.id)
- **sku**: VARCHAR
- **price**: DECIMAL
- **discount_price**: DECIMAL (nullable)
- **stock_quantity**: INT
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)
- weight
- dimensions

> _Nếu sản phẩm không có variant, tạo một bản ghi variant mặc định dựa trên base_price._

### **VariantAttributeValues**

- **variant_id**: INT (FK → ProductVariants.id)
- **attribute_id**: INT (FK → Attributes.id)
- **attribute_value_id**: INT (FK → AttributeValues.id)  
    _Primary Key: (variant_id, attribute_id, attribute_value_id)_

### **Attributes**

- **id**: INT (PK)
- **name**: VARCHAR
- **normalized_name**: VARCHAR
- **is_global**: BOOLEAN
- **merged_into_global_id**: INT (nullable, FK → Attributes.id)
- **created_by_vendor_id**: INT (FK → Vendors.id)
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### **AttributeValues**

- **id**: INT (PK)
- **attribute_id**: INT (FK → Attributes.id)
- **value**: VARCHAR
- **normalized_value**: VARCHAR
- **is_global**: BOOLEAN
- **merged_into_global_id**: INT (nullable, FK → AttributeValues.id)
- **created_by_vendor_id**: INT (FK → Vendors.id)
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### **ProductAttributes**

- **product_id**: INT (FK → Products.id)
- **attribute_id**: INT (FK → Attributes.id)  
    _Primary Key: (product_id, attribute_id)_

---

## 4. Review của Sản phẩm

### **ProductReviews**

- **id**: INT (PK)
- **product_id**: INT (FK → Products.id)
- **user_id**: INT (FK → Users.id)
- **rating**: DECIMAL _(hoặc INT)_
- **review_text**: TEXT
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### **ProductReviewMedia**

_Bảng này lưu trữ media (ảnh và video) kèm theo review._

- **id**: INT (PK)
- **review_id**: INT (FK → ProductReviews.id)
- **media_type**: VARCHAR  
    _(Cho phép "image" hoặc "video")_
- **media_url**: VARCHAR
- **alt_text**: VARCHAR
- **created_at**: DATETIME
- **updated_at**: DATETIME

---

## 5. Giỏ hàng

### **Carts**

- **id**: INT (PK)
- **user_id**: INT (FK → Users.id)
- **created_at**: DATETIME
- **updated_at**: DATETIME

### **CartItems**

- **id**: INT (PK)
- **cart_id**: INT (FK → Carts.id)
- **variant_id**: INT (FK → ProductVariants.id)
- **quantity**: INT
- **created_at**: DATETIME
- **updated_at**: DATETIME

---

## 6. Đơn hàng & Giao dịch Vendor

### **Orders**

- **id**: INT (PK)
- **user_id**: INT (FK → Users.id)  
    _(Khách hàng đặt hàng)_
- **shipping_address_id**: INT (FK → Addresses.id)  
    _(Địa chỉ giao hàng của khách hàng)_
- **order_date**: DATETIME
- **total_amount**: DECIMAL
- **order_status**: VARCHAR
- **payment_status**: VARCHAR
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### **VendorOrders**

- **id**: INT (PK)
- **vendor_id**: INT (FK → Vendors.id)
- **order_id**: INT (FK → Orders.id)
- **vendor_address_id**: INT (FK → Addresses.id)  
    _(Snapshot địa chỉ của vendor tại thời điểm order)_
- **order_date**: DATETIME
- **sub_total**: DECIMAL
- **status**: VARCHAR
- **tracking_number**: VARCHAR
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)
- shipping_method
- shipping_cost
- discount_amount
- notes
### **OrderItems**

- **id**: INT (PK)
- **vendor_order_id**: INT (FK → VendorOrders.id)
- **variant_id**: INT (FK → ProductVariants.id)
- **quantity**: INT
- **price_at_purchase**: DECIMAL
- **created_at**: DATETIME

---

## 7. Địa chỉ Chung (Addresses)

_Dùng chung cho khách hàng và vendor (vendor là user)_

- **id**: INT (PK)
- **user_id**: INT (FK → Users.id)
- **recipient_name**: VARCHAR
- **address_line**: VARCHAR
- **city**: VARCHAR
- **state_province**: VARCHAR
- **zip_code**: VARCHAR
- **country**: VARCHAR
- **created_at**: DATETIME
- **updated_at**: DATETIME
- address_type
- is_default

---

## 8. Thanh toán

### **PaymentMethods**

- **id**: INT (PK)
- **user_id**: INT (FK → Users.id)
- **payment_type**: VARCHAR  
    _(Ví dụ: "credit_card", "cod", "paypal", "bank_transfer")_
- **details**: TEXT or JSON
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### **PaymentTransactions**

- **id**: INT (PK)
- **order_id**: INT (FK → Orders.id)
- **payment_method_id**: INT (FK → PaymentMethods.id)
- **transaction_status**: VARCHAR  
    _(Ví dụ: "pending", "completed", "failed")_
- **transaction_date**: DATETIME
- **amount**: DECIMAL
- **tracking_number**: VARCHAR (nullable)
- **payment_response**: TEXT or JSON
- **created_at**: DATETIME
- **updated_at**: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### DiscountCodes:

- id: INT (Primary Key)
- code: VARCHAR
- description: TEXT
- discount_type: VARCHAR (giá trị: "percentage" hoặc "fixed_amount")
- discount_value: DECIMAL
- applicable_to
- min_order_value: DECIMAL (nullable)
- max_discount_amount: DECIMAL (nullable)
- start_date: DATETIME
- end_date: DATETIME
- usage_limit: INT (nullable)
- used_count: INT
- is_active: BOOLEAN
- created_by: INT (Foreign Key → Users.id)
- created_at: DATETIME
- updated_at: DATETIME
- is_deleted: BOOLEAN DEFAULT 0
- deleted_at: DATETIME (nullable)

### DiscountCodeConditions:

- id: INT (Primary Key)
- discount_code_id: INT (Foreign Key → DiscountCodes.id)
- condition_type: VARCHAR (giá trị: "min_quantity", "specific_category", "specific_vendor", "min_order_items")
- condition_value: VARCHAR
- created_at: DATETIME
- updated_at: DATETIME

Ví dụ 1: Mã giảm giá của vendor với điều kiện số lượng tối thiểu DiscountCodes:

- id: 1
- code: VENDOR_MIN5
- description: Giảm 15% cho sản phẩm của vendor nếu mua từ 5 sản phẩm trở lên
- discount_type: percentage
- discount_value: 15
- min_order_value: 0
- max_discount_amount: 50
- start_date: 2025-12-01 00:00:00
- end_date: 2025-12-31 23:59:59
- usage_limit: 100
- used_count: 0
- is_active: 1
- created_by: 200 (user_id của vendor)
- created_at: 2025-11-20 10:00:00
- updated_at: 2025-11-20 10:00:00

DiscountCodeScopes:

- id: 1
- discount_code_id: 1
- scope_type: vendor
- scope_value: 10 (vendor_id)
- created_at: 2025-11-20 10:00:00
- updated_at: 2025-11-20 10:00:00

DiscountCodeConditions:

- id: 1
- discount_code_id: 1
- condition_type: min_quantity
- condition_value: 5
- created_at: 2025-11-20 10:00:00
- updated_at: 2025-11-20 10:00:00

Ví dụ 2: Mã giảm giá của admin với điều kiện danh mục cụ thể DiscountCodes:

- id: 2
- code: TECH20
- description: Giảm 20 USD cho các sản phẩm thuộc danh mục công nghệ khi mua từ 100 USD
- discount_type: fixed_amount
- discount_value: 20
- min_order_value: 100
- max_discount_amount: NULL
- start_date: 2025-11-01 00:00:00
- end_date: 2025-11-30 23:59:59
- usage_limit: NULL
- used_count: 0
- is_active: 1
- created_by: 100 (user_id của admin)
- created_at: 2025-10-25 09:00:00
- updated_at: 2025-10-25 09:00:00

DiscountCodeScopes:

- id: 2
- discount_code_id: 2
- scope_type: category
- scope_value: 5 (category_id của danh mục công nghệ)
- created_at: 2025-10-25 09:00:00
- updated_at: 2025-10-25 09:00:00

DiscountCodeConditions:

- id: 2
- discount_code_id: 2
- condition_type: specific_category
- condition_value: 5↳
- created_at: 2025-10-25 09:00:00
- updated_at: 2025-10-25 09:00:00

Ví dụ 3: Mã giảm giá toàn hệ thống với điều kiện số mặt hàng tối thiểu DiscountCodes:

- id: 3
- code: SUMMER10
- description: Giảm 10% cho đơn hàng có ít nhất 3 mặt hàng
- discount_type: percentage
- discount_value: 10
- min_order_value: NULL
- max_discount_amount: 30
- start_date: 2025-07-01 00:00:00
- end_date: 2025-07-31 23:59:59
- usage_limit: 500
- used_count: 0
- is_active: 1
- created_by: 100 (user_id của admin)
- created_at: 2025-06-20 08:00:00
- updated_at: 2025-06-20 08:00:00

DiscountCodeScopes:

- id: 3
- discount_code_id: 3
- scope_type: global
- scope_value: NULL
- created_at: 2025-06-20 08:00:00
- updated_at: 2025-06-20 08:00:00

DiscountCodeConditions:

- id: 3
- discount_code_id: 3
- condition_type: min_order_items
- condition_value: 3
- created_at: 2025-06-20 08:00:00
- updated_at: 2025-06-20 08:00:00