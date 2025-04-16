---
title: System.Exception Base Class
tags:
  - C♯
---

> [!DEFINITION] 👌
> ***System.Exception*** class là base class của tất cả các loại exception khác

#### Các thuộc tính (Properties)
###### Message
- Là một ***string***, mô tả lí do gây ra exception
- Được viết ra cho các developer sẽ handle exception
- Nội dung của nó nên mô tả được toàn bộ error, mô tả được các chữa lỗi này
- Đôi khi sẽ hiện lên cho người dùng, đôi khi sẽ được log lại
###### StackTrace
- Là một string, chứa thông tin về callstack - stack các method call gây ra exception
- Giúp thấy được execution path/flow gây ra exception.
###### Data
- Là một IDictionary, với String key, Object value
- ..... (add later)
###### InnerException
- Chứa exception trước trong exception mới
- Exception "Wrapping"
###### Source
 - String chứa Application/Object name gây ra error
###### HResult
###### HelpLink
###### TargetSite
