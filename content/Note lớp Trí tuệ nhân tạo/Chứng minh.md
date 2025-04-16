# Phương Pháp Chứng Minh trong Logic Mệnh Đề

## 1. Chứng Minh Diễn Dịch (Direct Proof)

**Ý tưởng:**  
Bắt đầu từ các tiên đề đã cho và sử dụng các luật suy diễn (như Modus Ponens, luật đưa vào hội, tách khỏi hội, …) để "dẫn" trực tiếp ra định lý cần chứng minh.

**Ví dụ:**

Giả sử ta có các tiên đề:
1. $( Q \wedge S \to G \wedge H )$
2. $( P \to Q )$
3. $( R \to S )$
4. $( P )$
5. $( R )$

**Mục tiêu:** Chứng minh rằng $( G )$ đúng.

**Các bước chứng minh:**
1. Từ tiên đề (2) và (4):  
   Vì $( P \to Q )$ và $( P )$ đúng, nên theo **Luật Modus Ponens** suy ra $( Q )$.

2. Từ tiên đề (3) và (5):  
   Vì $( R \to S )$ và $( R )$ đúng, theo **Luật Modus Ponens** suy ra $( S )$.

3. Từ $( Q )$ và $( S )$:  
   Dùng **Luật Đưa Vào Hội** (Conjunction Introduction) để kết hợp thành $( Q \wedge S )$.

4. Từ tiên đề (1) và $( Q \wedge S )$:  
   $( Q \wedge S \to G \wedge H )$ cùng với $( Q \wedge S )$ đúng, áp dụng **Modus Ponens** để suy ra $( G \wedge H )$.

5. Từ $( G \wedge H )$:  
   Dùng **Luật Tách Khỏi Hội** (Conjunction Elimination) để lấy ra $( G )$.

Như vậy, ta đã chứng minh được $( G )$ thông qua các bước suy diễn trực tiếp từ các tiên đề.

---

## 2. Chứng Minh Bác Bỏ (Proof by Contradiction)

**Ý tưởng:**  
Để chứng minh một mệnh đề $( P )$ đúng, ta giả sử $( P )$ sai (tức giả sử $( \neg P )$ đúng) và sau đó dẫn ra mâu thuẫn (câu rỗng $( \bot )$). Khi có mâu thuẫn, ta kết luận giả sử ban đầu là sai, do đó $( P )$ phải đúng.

**Ví dụ:**

Giả sử muốn chứng minh $( G )$ đúng với cùng các tiên đề như trên:
1. $( Q \wedge S \to G \wedge H )$
2. $( P \to Q )$
3. $( R \to S )$
4. $( P )$
5. $( R )$

**Các bước chứng minh bác bỏ:**
1. Giả sử ngược lại, tức là giả sử $( \neg G )$ đúng.
2. Từ tiên đề (2) và (4), theo **Modus Ponens** suy ra $( Q )$.
3. Từ tiên đề (3) và (5), theo **Modus Ponens** suy ra $( S )$.
4. Từ $( Q )$ và $( S )$, ta có $( Q \wedge S )$.
5. Áp dụng tiên đề (1): $( Q \wedge S \to G \wedge H )$, suy ra $( G \wedge H )$. Từ đó, theo **Luật Tách Khỏi Hội**, ta có $( G )$ đúng.
6. Tuy nhiên, ta lại có giả thiết ban đầu $( \neg G )$. Như vậy, ta có $( G )$ và $( \neg G )$ cùng đúng, tạo nên mâu thuẫn (ký hiệu $( \bot )$).
7. Do mâu thuẫn xảy ra, kết luận rằng giả sử $( \neg G )$ là sai, nên $( G )$ phải đúng.

---

## 3. Luật Phân Giải (Resolution Rule)

**Ý tưởng:**  
Luật phân giải là một kỹ thuật suy diễn đặc biệt hữu ích trong việc chứng minh bằng phương pháp bác bỏ, đặc biệt khi các công thức đã được đưa về dạng chuẩn hội (CNF). Luật này cho phép “loại bỏ” một literal xuất hiện với hai dấu đối lập trong hai câu tuyển khác nhau.

**Cú pháp tổng quát:**  
Giả sử có hai câu tuyển:
- $( A_1 \vee A_2 \vee \dots \vee A_m \vee C )$
- $( B_1 \vee B_2 \vee \dots \vee B_n \vee \neg C )$

Áp dụng luật phân giải sẽ cho ta:
- $( A_1 \vee A_2 \vee \dots \vee A_m \vee B_1 \vee B_2 \vee \dots \vee B_n )$

**Ví dụ đơn giản:**  
Cho các câu tuyển:
- $( A \vee B )$
- $( \neg B \vee C )$

Ta có thể loại bỏ $( B )$ bằng cách phân giải, suy ra:
- $( A \vee C )$

---

## 4. Chứng Minh Bác Bỏ Bằng Luật Phân Giải (Refutation Using Resolution)

**Ý tưởng:**  
Khi sử dụng phương pháp này, ta:
1. Đưa tất cả các tiên đề về dạng CNF (dạng chuẩn hội).
2. Thêm vào tập tiên đề phủ định của kết luận cần chứng minh.
3. Áp dụng luật phân giải liên tục cho đến khi ta có thể sinh ra câu rỗng $( \bot )$ (mâu thuẫn).

**Ví dụ chi tiết:**

Giả sử ta cần chứng minh $( G )$ đúng từ các tiên đề:
1. $( Q \wedge S \to G \wedge H )$
2. $( P \to Q )$
3. $( R \to S )$
4. $( P )$
5. $( R )$

**Bước 1: Chuyển các công thức về dạng CNF**

- Tiên đề (1):  
  $( Q \wedge S \to G \wedge H )$  
  Dùng định nghĩa $( A \to B \equiv \neg A \vee B )$:
  $[  \neg (Q \wedge S) \vee (G \wedge H)]$
  Sử dụng luật De Morgan:  
  $[
  (\neg Q \vee \neg S) \vee (G \wedge H)
  ]$
  Áp dụng phân phối, ta tách thành hai câu tuyển:
  - $( \neg Q \vee \neg S \vee G )$  
  - $( \neg Q \vee \neg S \vee H )$

- Tiên đề (2):  
  $( P \to Q \equiv \neg P \vee Q )$

- Tiên đề (3):  
  $( R \to S \equiv \neg R \vee S )$

- Tiên đề (4): $( P )$ (đã ở dạng literal)

- Tiên đề (5): $( R )$ (đã ở dạng literal)

**Bước 2: Thêm phủ định của kết luận cần chứng minh**

Mục tiêu là chứng minh $( G )$ đúng. Ta thêm:
- $( \neg G )$

**Tập các câu tuyển (clauses) ban đầu là:**

1. $( \neg Q \vee \neg S \vee G )$
2. $( \neg Q \vee \neg S \vee H )$  (thường không dùng nếu chỉ cần chứng minh $( G )$)
3. $( \neg P \vee Q )$
4. $( \neg R \vee S )$
5. $( P )$
6. $( R )$
7. $( \neg G )$  (phủ định kết luận)

**Bước 3: Áp dụng Luật Phân Giải**

- Từ (3) và (5):  
  $( \neg P \vee Q )$ và $( P )$ cho ta loại bỏ $( P )$ bằng phân giải, suy ra:
  - $( Q )$

- Từ (4) và (6):  
  $( \neg R \vee S )$ và $( R )$ cho ta loại bỏ $( R )$, suy ra:
  - $( S )$

- Với $( Q )$ và $( S )$ biết được, ta xét câu tuyển (1):  
  $( \neg Q \vee \neg S \vee G )$  
  Vì $( Q )$ và $( S )$ đều đúng nên $( \neg Q )$ và $( \neg S )$ đều sai, câu tuyển này buộc phải có $( G )$ đúng.  
  Tuy nhiên, ta lại có câu (7): $( \neg G )$.

Khi ta phân giải giữa $( G )$ (từ (1) và sự thật $( Q, S )$) và $( \neg G )$ (câu (7)), ta thu được mâu thuẫn (câu rỗng $( \bot )$).  
Điều này chứng tỏ rằng tập các câu tuyển ban đầu (khi thêm $( \neg G )$) là không thoả được. Do đó, theo nguyên lý của **chứng minh bác bỏ bằng phân giải**, kết luận $( G )$ phải đúng.

---

# Tổng Kết

- **Chứng minh diễn dịch** sử dụng các bước suy diễn trực tiếp từ tiên đề để dẫn ra kết luận.
- **Chứng minh bác bỏ** dựa vào giả sử ngược và tìm mâu thuẫn để khẳng định tính đúng của định lý.
- **Luật phân giải** là một công cụ mạnh mẽ để xử lý các câu tuyển sau khi đã đưa về dạng CNF.
- **Chứng minh bác bỏ bằng luật phân giải** kết hợp việc chuyển đổi các công thức sang dạng CNF, thêm phủ định kết luận, và áp dụng luật phân giải liên tục để dẫn ra mâu thuẫn.

Những ví dụ trên minh họa quy trình chi tiết của từng phương pháp. Bạn có thể áp dụng các bước này vào các bài toán logic phức tạp hơn để chứng minh các định lý khác.
