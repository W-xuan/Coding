#### [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

 

**示例 1：**

```
输入：n = 3
输出：3
```

**示例 2：**

```
输入：n = 11
输出：0
```

 ```C++
 class Solution {
 public:
     int findNthDigit(int n) {
         int digit = 1;
         long long start = 1;
         long long cnt = 9; 
         while (n > cnt) {
             n -= cnt;
             ++digit;
             start *= 10;
             cnt = 9 * start * digit;
         }
         n--;
         int ans = to_string(num)[n % digit] - '0';
         return ans;
     }
 };
 ```
```C++
class Solution {
public:
    int digitAtIndex(int n) {
        long long i = 1, num = 9, base = 1;
        while (n > i * num) {
            n -= i * num;
            i ++;
            num *= 10;
            base *= 10;
        }

        int number = base + (n + i - 1) / i - 1;
        int r = n % i ? n % i : i;
        for (int j = 0; j < i - r; j ++ ) number /= 10;
        return number % 10;
    }
};
```