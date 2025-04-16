---
title: Value Object
tags:
  - architectures
  - Full-Stack
---
### **Value Object trong Clean Architecture là gì?**

#### **1. Định nghĩa**

- **Value Object (VO)** là một đối tượng **không có ID duy nhất**, được xác định bởi **giá trị của các thuộc tính** thay vì danh tính (identity).
- Value Object **không thể thay đổi trạng thái** (**immutable**), có nghĩa là khi muốn thay đổi một giá trị, ta phải tạo một đối tượng mới thay vì thay đổi đối tượng hiện có.
- Value Object thường được dùng để đại diện cho **một khái niệm hoặc một nhóm thuộc tính có ý nghĩa** trong nghiệp vụ.

---
#### **2. Khác biệt giữa Value Object và Entity**

|**Tiêu chí**|**Entity**|**Value Object**|
|---|---|---|
|**Danh tính (ID)**|Có ID duy nhất để phân biệt.|Không có ID, được phân biệt bằng giá trị của các thuộc tính.|
|**Thay đổi trạng thái**|Có thể thay đổi trạng thái.|Bất biến (immutable), không thay đổi sau khi được tạo.|
|**Sử dụng trong hệ thống**|Đại diện cho một thực thể có vòng đời riêng.|Đại diện cho một tập hợp các thuộc tính có ý nghĩa.|
|**Ví dụ**|`Customer`, `Order`, `Product`.|`Address`, `Money`, `DateRange`.|

#### **3. Ví dụ về Value Object trong C#**

##### **Ví dụ 1: Đối tượng `Money` để biểu diễn tiền tệ**

``` c#
public class Money
{
    public decimal Amount { get; }
    public string Currency { get; }

    public Money(decimal amount, string currency)
    {
        if (amount < 0) throw new ArgumentException("Số tiền không thể âm.");
        if (string.IsNullOrWhiteSpace(currency)) throw new ArgumentException("Đơn vị tiền tệ không hợp lệ.");

        Amount = amount;
        Currency = currency;
    }

    public Money Add(Money other)
    {
        if (Currency != other.Currency)
            throw new InvalidOperationException("Không thể cộng hai loại tiền khác nhau.");

        return new Money(Amount + other.Amount, Currency);
    }

    public override bool Equals(object obj)
    {
        if (obj is Money money)
        {
            return Amount == money.Amount && Currency == money.Currency;
        }
        return false;
    }

    public override int GetHashCode()
    {
        return HashCode.Combine(Amount, Currency);
    }
}
```

**Điểm quan trọng:**  
✅ **Không có ID** – Được so sánh dựa trên giá trị của `Amount` và `Currency`.  
✅ **Immutable** – Khi muốn thay đổi giá trị, ta phải tạo một đối tượng mới (`Add` tạo một `Money` mới).  
✅ **So sánh bằng giá trị**, không phải bằng tham chiếu (`Equals` và `GetHashCode` được ghi đè).

#### **4. Khi nào sử dụng Value Object?**

✔ Khi đối tượng **không cần ID duy nhất** và chỉ cần so sánh dựa trên giá trị.  
✔ Khi muốn đảm bảo **bất biến (immutability)** để tránh lỗi do thay đổi dữ liệu không mong muốn.  
✔ Khi cần **tách biệt logic nghiệp vụ** vào các đối tượng chuyên biệt (ví dụ: `Money`, `Address`, `DateRange`).  
✔ Khi cần sử dụng đối tượng **như một phần của một Entity khác** nhưng không phải là một Entity độc lập.

---

### **5. Kết luận**

- **Value Object KHÔNG có ID, trong khi Entity có ID.**
- **Value Object là bất biến (immutable), Entity có thể thay đổi trạng thái.**
- **Value Object nên được dùng khi một tập hợp thuộc tính có ý nghĩa nghiệp vụ nhưng không cần được theo dõi như một thực thể riêng biệt.**
- **Trong Clean Architecture, Value Object giúp mã nguồn dễ bảo trì, dễ test, và giảm lỗi do dữ liệu bị thay đổi ngoài ý muốn.**