#### [剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

**示例:**

```
输入: a = 1, b = 1
输出: 2
```

```C++
class Solution {
public:
    int add(int a, int b) {
        return b ? add(a ^ b, (unsigned)(a & b) << 1) : a;
    }
};
```

```cpp
class Solution {
public:
    int add(int num1, int num2){
        while(num2) {
            int sum = num1 ^ num2;
            int carry = (num1 & num2) << 1;
            num1 = sum;
            num2 = carry;
        }
        return num1;
    }
};
```
