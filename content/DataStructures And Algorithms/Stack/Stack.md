---
title: Stack
tags:
  - DataStructures
---
>***<span style="color:rgb(135, 70, 200)">Stack***</span> là cấu trúc dữ liệu tập hợp hỗ trợ ***FILO (First In Last Out)***

#### Ví dụ sử dụng stack
- [Bài toán check ngoặc](https://leetcode.com/problems/valid-parentheses/description/)
- Solution:
``` c#
public class Solution {
    public bool IsValid(string s) {
        Stack<char> container = new();
        foreach (char c in s)
        {
            if (c == '(' || c == '{' || c == '[')  //if c is open parenthesis
            {
                container.Push(c);     //push it into stack
            }
            else            //else (close one)
            {
                if (container.Count == 0)    // if now stack have nothing (even its closing one)
                {
                    return false;          // so it's false
                }
                char last = container.Pop();   // else, we pop the last one
                if ((last == '(' && c != ')') || (last == '[' && c != ']') || (last == '{' && c != '}'))    //compare!!
                {
                    return false;
                }
            }
        }
        return container.Count == 0 ? true : false;  //if there are still parentheses havent been closed, it false, true other wise
    }
}
```
#### Visualize stack
- [Stack tạo bằng Array](https://www.cs.usfca.edu/~galles/visualization/StackArray.html)
- [Stack tạo bằng Linked List](https://www.cs.usfca.edu/~galles/visualization/StackLL.html)
#### My source code :>
- [Stack (Cả array based và linked list based)](https://github.com/HoangDucHiep/Coursera---Data-Structures-and-Algorithms-Specialization/tree/main/Data_Structures/data_structure_implementations/stack_queue_deque/c_sharp/Stack)
#### Giải thích
