---
title: HTTP
tags:
  - Full-Stack
---
#### <span style="color:rgb(184, 123, 234)">Safety và</span> <span style="color:rgb(184, 123, 234)">Idempotency</span>
- Safety - việc thực thi một request mà không gây ra side effects cho server
- Như GET, hay HEAD, chúng chỉ lấy dữ liệu từ server và trả về Response chứ không gây tác động gì đến server
- Idempotence - Việc thực hiện N lần một request nhất định mà luôn tạo ra 1 kết quả duy nhất, GET, HEAD, PUT, DELETE đạt được tính chất này, POST thì không