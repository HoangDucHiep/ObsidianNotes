---
title: Document-oriented databases
tags:
  - Database
  - NoSQL
---
### Document-oriented databases là gì
- <span style="font-weight:bold; color:rgb(184, 123, 234)">Document-oriented databases</span> *là* một loại cơ sở dữ liệu ***NoSQL***
- Nó lưu trữ dữ liệu trong các documents dưới dạng tương tự như JSON objects
- Mỗi documents chứa các cặp <span style="font-weight:bold; color:rgb(184, 123, 234)">fields</span> và <span style="font-weight:bold; color:rgb(184, 123, 234)">values</span>
- Các <span style="font-weight:bold; color:rgb(184, 123, 234)">values</span> có thể thuộc ***nhiều kiểu khác nhau***, bao gồm chuỗi, số, boolean, mảng hoặc thậm chí các đối tượng khác
``` JSON
{ 
	"_id": 1, 
	"first_name": "Tom", 
	"email": "tom@example.com", 
	"cell": "765-555-5555", 
	"likes": [ "fashion", "spas", "shopping" ], 
	"businesses": [ 
		{ 
			"name": "Entertainment 1080", 
			"partner": "Jean", 
			"status": "Bankrupt", 
			"date_founded": { 
				"$date": "2012-05-19T04:00:00Z" 
			} 
		}, 
		{ 
			"name": "Swag for Tweens", 
			"date_founded": { 
				"$date": "2012-11-01T04:00:00Z" 
			}
		} 
	]
}
```

### Collections
- Là một nhóm các documents
- Collections thường chứa các documents có nội dung tương tự nhau
- Không phải tất cả các tài liệu trong một bộ sưu tập đều phải có cùng các trường, vì cơ sở dữ liệu tài liệu có lược đồ linh hoạt
- Không phải tất cả các documents trong một collections đều phải có cùng các fields, vì document databases có [lược đồ](Schema) linh hoạt
``` js
db.users.insertMany([
    {
        "name": "Trần Thị B",
        "email": "tranthib@example.com",
        "age": 30
    },
    {
        "name": "Lê Văn C",
        "email": "levanc@example.com",
        "age": 28,
        "address": "Hà Nội"
    }
])
```


### Đặc điểm chính của Document-oriented databases
- <span style="font-weight:bold; color:rgb(184, 123, 234)">Document model</span>: Dữ liệu được lưu trữ trong các documents, ánh xạ tới các đối tượng trong hầu hết các ngôn ngữ lập trình phổ biến, cho phép các nhà phát triển nhanh chóng phát triển ứng dụng của họ. Các định dạng phổ biến để lưu trữ tài liệu bao gồm JSON, BSON và XML
- <span style="font-weight:bold; color:rgb(184, 123, 234)">Flexible schema</span>: 
	- Document databases có lược đồ linh hoạt, nghĩa là ***không phải tất cả các tài liệu trong một tập hợp đều cần có cùng các trường***
	- Một số cơ sở dữ liệu tài liệu hỗ trợ [schema validation](https://docs.mongodb.com/manual/core/schema-validation/), vì vậy lược đồ có thể được khóa tùy chọn khi cần
- <span style="font-weight:bold; color:rgb(184, 123, 234)">Distributed and resilient</span>: 
	- Document databases được phân tán, cho phép nó có thể mở trong dọc (Horizontal scaling) và phân tán dữ liệu
	- Document databases có thể phục hồi thông qua sao chép
- **<span style="color:rgb(184, 123, 234)">Querying through an API or query language</span>**:
	- Document databases có API hoặc ngôn ngữ truy vấn cho phép các nhà phát triển thực hiện các hoạt động CRUD trên cơ sở dữ liệu. 
	- Các nhà phát triển có khả năng truy vấn các tài liệu dựa trên unique identifiers hoặc field values.