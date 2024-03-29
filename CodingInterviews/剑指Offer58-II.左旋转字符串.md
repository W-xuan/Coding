#### [剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

```c++
class Solution {
public:
    string reverseLeftwords(string s, int n) {
        char temp[s.size() + 1];
        for (int i = 0; i < n; ++i) {
            temp[i + s.size() - n] = s[i];
        }
        for (int i = n; i < s.size(); ++i) {
            temp[i - n] = s[i];
        }
        temp[s.size()] = '\0';
        return temp;
    }
};
```

```
C++
class Solution {
public:
    string leftRotateString(string str, int n) {
        reverse(str.begin(), str.end());
        reverse(str.begin(), str.begin() + str.size() - n);
        reverse(str.begin() + str.size() - n, str.end());
        return str;
    }
};
```
