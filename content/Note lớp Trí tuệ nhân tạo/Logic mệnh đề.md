## 1. Khái Niệm Cơ Bản

### 1.1. Mệnh Đề
- **Định nghĩa:**  
  Mệnh đề là một phát biểu có thể xác định được tính ***đúng*** hay ***sai***.
- **Ví dụ:**  
  - **P:** “Hà Nội là thủ đô của Việt Nam” <span style="color:rgb(133, 255, 135)">(Đúng)  </span>
  - **Q:** “Số 6 là số nguyên tố”<span style="color:rgb(255, 0, 0)"> (Sai)</span>

---

## 2. Cú Pháp và Ngữ Nghĩa của Logic Mệnh Đề

### 2.1. Cú Pháp
- **Các ký hiệu cơ bản:**
  - **Hằng logic:** `True` và `False`
  - **Biến mệnh đề:** P, Q, R, …  
  - **Kết nối logic:**
    - `∧` (và - AND)
    - `∨` (hoặc - OR)
    - `¬` (phủ định - NOT)
    - `→` (kéo theo - IMPLICATION)
    - `↔` (tương đương - BICONDITIONAL)
  - **Dấu ngoặc:** Dùng để nhóm các biểu thức.

- **Quy tắc xây dựng công thức:**  
  - Mỗi biến mệnh đề là một công thức cơ bản.
  - Nếu A và B là công thức, ta có thể tạo ra:
    - `(A ∧ B)` đọc là “A và B” hoặc "A hội B"
    - `(A ∨ B)` đọc là “A hoặc B” hoặc "A tuyển B"
    - `¬A` đọc là “phủ định A”
    - `(A → B)` đọc là “nếu A thì B” hoặc "A kéo theo B"
    - `(A ↔ B)` đọc là “A và B kéo theo nhau”

- **Chú ý:**  
  - **Công thức đơn:** Các biến mệnh đề hoặc literal (ví dụ: P, ¬P)  
  - **Công thức phức hợp:** Các công thức được tạo ra từ các kết nối logic (ví dụ: `(P ∨ Q)`, `(P ∧ Q)`)

### 2.2. Ngữ Nghĩa
- **Ý nghĩa của công thức:**  
  Xác định bằng cách **minh họa** (interpretation) – gán mỗi biến mệnh đề một giá trị chân lý (`True` hoặc `False`).

- **Minh họa:**  
  Ví dụ, gán P với “Paris là thủ đô của Pháp” để xác định tính đúng/sai của các công thức chứa P.

- **Bảng chân lý:**  
  Giúp xác định giá trị chân lý của các công thức dựa vào giá trị của các biến mệnh đề.

| $P$                                                   | $Q$                                                   | $¬P$                                                  | $P ∧ Q$                                               | $P ∨ Q$                                               | $P → Q$                                               | $P ↔ Q$                                               |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> |
| <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     |
| <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     |
| <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> |
- **Các khái niệm liên quan:**  
  - **Thoả được (Satisfiable):** Có tồn tại ít nhất một cách gán giá trị làm cho công thức đúng.  
  - **Vững chắc (Tautology):** Công thức luôn đúng với mọi cách gán.  
  - **Không thoả được (Unsatisfiable):** Công thức luôn sai với mọi cách gán
- Vd: Xác định ngữ nghĩa của $(P → Q) ∧ S$ (Thỏa được không vững chắc)

| $P$                                                   | $Q$                                                   | $S$                                                   | $P → Q$                                               | $(P → Q) ∧ S$                                         |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     |
| <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> |
| <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     |
| <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> |
| <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     |
| <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(255, 0, 0)">***F***</span>     |
| <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(255, 0, 0)">***F***</span>     |
| <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> | <span style="color:rgb(133, 255, 135)">***T***</span> |

---
## Sự Tương Đương của Các Công Thức

- Hai công thức **A** và **B** được xem là **tương đương** nếu chúng có cùng giá trị chân lý trong mọi minh họa. Ký hiệu:  
	**A ≡ B**

### Một số định nghĩa và định lý cơ bản:

- **A → B ≡ ¬A ∨ B**  (Nếu A thì B tương đương với "phủ định A hoặc B")

- **A ↔ B ≡ (A → B) ∧ (B → A)**  (A kéo theo B và ngược lại tương đương với việc cả A → B và B → A đều đúng)

- **¬(¬A) ≡ A**  (Phủ định của phủ định A tương đương với A)

### Một số luật biến đổi tương đương:

1. **Luật De Morgan:**
   - ¬(A ∨ B) ≡ ¬A ∧ ¬B
   - ¬(A ∧ B) ≡ ¬A ∨ ¬B

2. **Luật giao hoán (Commutative Laws):**
   - A ∨ B ≡ B ∨ A
   - A ∧ B ≡ B ∧ A

3. **Luật kết hợp (Associative Laws):**
   - (A ∨ B) ∨ C ≡ A ∨ (B ∨ C)
   - (A ∧ B) ∧ C ≡ A ∧ (B ∧ C)

4. **Luật phân phối (Distributive Laws):**
   - A ∧ (B ∨ C) ≡ (A ∧ B) ∨ (A ∧ C)
   - A ∨ (B ∧ C) ≡ (A ∨ B) ∧ (A ∨ C)

![[Pasted image 20250323142138.png]]
![[Pasted image 20250323142145.png]]

## 3. Dạng Chuẩn Tắc
### 3.1. Dạng Chuẩn Hội (CNF)
- **Định nghĩa:**  
  Công thức ở dạng chuẩn hội là **hội (AND)** của các câu tuyển (clause), trong đó mỗi câu tuyển là dạng:  
  `A1 ∨ A2 ∨ ... ∨ Am`  
  với mỗi `Ai` là một literal.

- **Các bước chuẩn hóa:**  
  1. **Bỏ dấu kéo theo:** Thay `(A → B)` bằng `(¬A ∨ B)`.
  2. **Đẩy phủ định vào trong:** Áp dụng luật De Morgan (ví dụ: `¬(A ∨ B) ≡ ¬A ∧ ¬B`).
  3. **Phân phối:** Biến đổi biểu thức theo quy tắc phân phối (ví dụ: `A ∨ (B ∧ C) ≡ (A ∨ B) ∧ (A ∨ C)`).

- **Ví dụ:**  
  Chuẩn hóa công thức `(P → Q) ∨ ¬(R ∨ ¬S)`:
  - Thay `P → Q` bằng `¬P ∨ Q`.
  - Áp dụng De Morgan: `¬(R ∨ ¬S) ≡ ¬R ∧ S`.
  - Sử dụng luật phân phối để đưa về dạng CNF:  
    `(¬P ∨ Q ∨ ¬R) ∧ (¬P ∨ Q ∨ S)`.

### 3.2. Dạng Chuẩn Horn
- **Định nghĩa:**  
  Là dạng đặc biệt của CNF, trong đó mỗi câu tuyển chứa tối đa một literal dương (không phủ định).  
  - **Ví dụ:**  
    `P1 ∧ P2 ∧ ... ∧ Pm → Q`  
    - Khi `m = 0`, câu Horn trở thành một câu đơn (Q).

- **Ý nghĩa:**  
  Dạng Horn quan trọng trong hệ thống suy diễn và lập trình logic (như Prolog).

---
## 4. Luật Suy Diễn và Phương Pháp Chứng Minh

### 4.1. Luật Suy Diễn Cơ Bản

- **Luật Modus Ponens:**  
  Từ `(A → B)` và `A` suy ra `B`.  
  *Ví dụ:* Nếu "Nếu học chăm thì điểm cao" và "Học chăm" đúng, thì suy ra "Điểm cao".

- **Luật Modus Tollens:**  
  Từ `(A → B)` và `¬B` suy ra `¬A`.

- **Luật Phân Giải (Resolution):**  
  Kỹ thuật loại bỏ literal đối lập giữa hai câu.  
  *Ví dụ:* Từ `(A ∨ B)` và `(¬B ∨ C)`, suy ra `(A ∨ C)`.

- **Luật Đưa Vào Hội (Conjunction Introduction):**  
  Từ `A` và `B`, suy ra `(A ∧ B)`.  
  *Ý nghĩa:* Nếu biết A đúng và B đúng, thì cả hai kết hợp lại cũng đúng.

- **Luật Tách Khỏi Hội (Conjunction Elimination):**  
  Từ `(A ∧ B)`, suy ra được cả `A` (hoặc `B`).  
  *Ý nghĩa:* Từ một công thức chứa "và" ta có thể lấy ra bất kỳ thành phần nào.

- **Luật Đưa Vào Tuyển (Disjunction Introduction):**  
  Từ `A`, suy ra `(A ∨ B)` với bất kỳ công thức nào `B`.  
  *Ý nghĩa:* Nếu A đúng thì "A hoặc B" luôn đúng, bất kể B là gì.

- **Luật Loại Bỏ Tuyển (Disjunction Elimination):**  
  Từ `(A ∨ B)`, nếu ta có thể chứng minh một kết luận `C` từ giả thiết `A` và cũng chứng minh được `C` từ giả thiết `B`, thì suy ra `C`.  
  *Ý nghĩa:* Dù A hay B đúng, kết luận C vẫn được suy ra.
![[Pasted image 20250323144942.png]]
 
### 4.2. Phương Pháp Chứng Minh

Có hai phương pháp chính:

- **Chứng minh diễn dịch (Direct Proof):**  
  Bắt đầu từ các tiên đề và sử dụng các luật suy diễn (như các luật nêu trên) để dẫn dắt ra định lý cần chứng minh.  
  *Ví dụ minh họa:*
  1. Từ `(P → Q)` và `P`, dùng Modus Ponens để suy ra `Q`.
  2. Từ `Q` và các tiên đề khác, suy ra định lý cần chứng minh.

- **Chứng minh bác bỏ (Proof by Contradiction/Refutation):**  
  Giả sử định lý cần chứng minh là sai (thêm `¬(Định lý)` vào tập tiên đề) và dẫn đến mâu thuẫn (câu rỗng `⊥`). Khi mâu thuẫn xuất hiện, kết luận rằng định lý ban đầu phải đúng.

### 4.3. Ví Dụ Chứng Minh

Giả sử có các tiên đề:
1. **(1)** `Q ∧ S → G ∧ H`
2. **(2)** `P → Q`
3. **(3)** `R → S`
4. **(4)** `P`
5. **(5)** `R`

**Chứng minh bằng phương pháp diễn dịch:**
1. Từ (2) và (4): Suy ra `Q` (Modus Ponens).
2. Từ (3) và (5): Suy ra `S`.
3. Từ `Q` và `S`: Dùng Luật Đưa Vào Hội để có `Q ∧ S`.
4. Từ (1) và `Q ∧ S`: Dùng Modus Ponens để suy ra `G ∧ H`.
5. Từ `G ∧ H`: Dùng Luật Tách Khỏi Hội để lấy ra `G`.

**Chứng minh bằng phương pháp bác bỏ:**
- Giả sử `G` sai (tức `¬G`).
- Chuẩn hóa các công thức về dạng câu tuyển.
- Áp dụng Luật Phân Giải (và các luật suy diễn khác nếu cần) cho đến khi sinh ra mâu thuẫn (câu rỗng `⊥`).
- Khi mâu thuẫn xuất hiện, kết luận rằng giả sử ban đầu sai, do đó `G` phải đúng.


## 5. Luật Phân Giải Nâng Cao

- **Áp dụng trên các câu tuyển:**  
  Luật phân giải cho phép kết hợp hai câu tuyển khi một trong các literal của câu này là đối lập với literal của câu kia.
  
- **Áp dụng trên các câu Horn:**  
  Đối với các câu Horn (dạng if-then), luật phân giải giúp rút ra kết luận dựa trên các điều kiện cho trước.

- **Ví dụ:**  
  Cho tập câu tuyển:
  1. `¬A ∨ ¬B ∨ P`
  2. `¬C ∨ ¬D ∨ P`
  3. `¬E ∨ C`
  4. `A`
  5. `E`
  6. `D`  
  Để chứng minh `P`, ta thêm `¬P` và sử dụng luật phân giải liên tục cho đến khi sinh ra câu rỗng. Khi đó, kết luận rằng `P` là hệ quả logic của tập tiên đề.

---

## 6. Bài Tập Thực Hành

1. **Bài tập 1:**  
   Cho tập công thức:  
   - (1) `P → Q`  
   - (2) `P ∨ R`  
   - (3) `¬Q`  
   - (4) `R → S`  
   
   **Yêu cầu:**  
   - Chuẩn hóa các công thức.
   - Lập bảng chứng minh S.

2. **Bài tập 2:**  
   Cho tập công thức:  
   - (1) `E → F`  
   - (2) `A ∧ B → C`  
   - (3) `B → D`  
   - (4) `C ∧ D → E`  
   - (5) `A`  
   - (6) `B`  
   
   **Yêu cầu:**  
   - Chuẩn hóa các công thức.
   - Lập bảng chứng minh F.

3. **Bài tập 3:**  
   Cho tập công thức:  
   - (1) `E → G`  
   - (2) `B ∧ E → I`  
   - (3) `A ∧ B → E`  
   - (4) `A ∧ G → C`  
   - (5) `G ∧ I → H`  
   - (6) `A`  
   - (7) `B`  
   
   **Yêu cầu:**  
   - Chứng minh H bằng phương pháp bác bỏ.

---

## Tổng Kết

- **Logic mệnh đề** gồm các thành phần cơ bản: mệnh đề, biến mệnh đề, kết nối logic và cách xây dựng công thức.
- **Ngữ nghĩa** được xác định qua minh họa (gán giá trị chân lý) và bảng chân lý.
- **Dạng chuẩn tắc:** CNF và Horn rất hữu ích trong việc chuẩn hóa công thức và ứng dụng vào lập luận.
- **Luật suy diễn** như Modus Ponens, Modus Tollens, và đặc biệt là luật phân giải đóng vai trò quan trọng trong quá trình chứng minh.
- Hai phương pháp chứng minh chính là **diễn dịch** và **bác bỏ**, giúp chúng ta xác định tính đúng đắn của các định lý dựa trên tập tiên đề.

Hy vọng hướng dẫn này sẽ giúp bạn nắm vững kiến thức về logic mệnh đề. Nếu có thắc mắc hay cần giải thích thêm ví dụ cụ thể, bạn hãy trao đổi thêm nhé!
