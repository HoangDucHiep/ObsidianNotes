---
title: Number theory
tags:
  - Cryptography_and_sercurity
---
## <span style="color:rgb(184, 123, 234)">Divisibility (khả năng chia hết)</span>

- Một số khác không ***b*** <span style="font-style:italic; font-weight:bold; color:rgb(184, 123, 234)">chia hết (divide)</span> cho số ***a*** nếu ***a = m.b*** (với một số ***a, b, m*** là số nguyên)
- Hay ***b*** chia hết cho ***a*** nếu không tạo ra dư sau khi chia

- Kí hiệu:
	$b\ |\ a$ :  **b**** chia hết cho ***a***, và ***b*** là *<span style="font-weight:bold; color:rgb(184, 123, 234)">divisor</span>* của ***a***
	
- Ví dụ:   $2\ |\ 4$: 2 chia hết cho 4

##### <span style="color:rgb(184, 123, 234)">Các tính chất của divisibility với số nguyên</span>

1. Nếu $a\ |\ 1$, thì $a\ =\ \pm1$ 
2. Nếu $a\ |\ b$ và $b\ |\ a$, thì $a\ = \pm b$
3.  $\forall b \neq 0$, $b\ |\ 0$
4. Nếu $a\ |\ b$ và $b\ |\ c$ , thì $a\ |\ c$
5. Nếu $b\ |\ g$ và $b\ |\ h$, thì $b\ |\ (mg\ +\ nh)$, với $m, n$ là số nguyên bất kì

##### <span style="color:rgb(184, 123, 234)">The Division Algoritm</span>
- $a\ =\ qn\ +\ r$            $0\leq r < n; q = \lfloor a/n \rfloor$
	- Với a, q, n, r là các số nguyên
	- $\lfloor x \rfloor$ : số nguyên lớn nhất ***nhỏ hơn hoặc bằng*** x
	- ***r*** thường được gọi là <span style="font-weight:bold; color:rgb(184, 123, 234)">residue</span> (dư)
 ![[Pasted image 20250210223320.png]]
![[Pasted image 20250210223335.png]]
## <span style="color:rgb(184, 123, 234)">Số học Modular</span>
##### <span style="color:rgb(184, 123, 234)">Modulus</span>
> [!NOTE] Modulus
> - Với số nguyên $a$ và số nguyên dương $n$, ta có $a\ mod\ n$ là phần dư của phép chia $a$ cho $n$
> - Số nguyên $n$ gọi là ***modulus*** (số chia)
> - Vậy với số nguyên a bất kì, ta có công thức:
>   $a\ = \ qn \ + \ r \quad \quad 0 \leq r < n;\ q = \lfloor a/n \rfloor$
>   $a\ = \lfloor a/n \rfloor \times n + (a\ mod\ n)$
- $11\ mod\ 7\ =\ 4$, $-11\ mod\ 7\ =\ 3$
##### <span style="color:rgb(184, 123, 234)">Congruent modulo (Đồng dư)</span>

> [!NOTE] Đồng dư
> - Hai số nguyên **a** và **b** được gọi là **đồng dư theo mô-đun n** (congruent modulo n) nếu chúng có cùng phần dư khi chia cho **n**:
> - **$(a\ mod\ n)\ =\ (b\ mod\ n)$** được viết như sau:
>  $a≡b(mod\ n)$
- $73\ ≡\ 4\ (mod\ 23)$
	$73\ mod\ 23\ =\ 4$ và $4\ mod\ 23\ =\ 4$
- Ta có nếu $a\ ≡\ 0\ (mod\ n)$ thì $n | a$ 
##### <span style="color:rgb(184, 123, 234)">Các tính chất của đồng dư</span>
6. $( a \equiv b \pmod{n} )$ nếu và chỉ nếu $( n \mid (a - b) )$. 
7. Nếu $( a \equiv b \pmod{n} )$, thì $( b \equiv a \pmod{n} )$. 
8. Nếu $( a \equiv b \pmod{n} )$ và $( b \equiv c \pmod{n} )$, thì $( a \equiv c \pmod{n} )$.
