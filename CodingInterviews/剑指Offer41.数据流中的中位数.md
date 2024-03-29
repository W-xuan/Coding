#### [剑指 Offer 41. 数据流中的中位数](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

- void addNum(int num) - 从数据流中添加一个整数到数据结构中。
- double findMedian() - 返回目前所有元素的中位数。

**示例 1：**

```
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]
```

**示例 2：**

```
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]
```

```cpp
class Solution {
public:
    priority_queue<int> max_heap;
    priority_queue<int, vector<int>, greater<int> > min_heap;
    void insert(int num){
       max_heap.push(num);
       while(min_heap.size() && min_heap.top() < max_heap.top()) {
           int minv = min_heap.top(), maxv = max_heap.top();
           min_heap.pop(), max_heap.pop();
           min_heap.push(maxv), max_heap.push(minv);
       }
       if (max_heap.size() > min_heap.size() + 1) {
           min_heap.push(max_heap.top()), max_heap.pop();
       }
    }

    double getMedian(){
        if (max_heap.size() + min_heap.size() & 1) return max_heap.top();
        return (max_heap.top() + min_heap.top()) / 2.0;
    }
};
```


```C++
 class MedianFinder {
 public:
     /** initialize your data structure here. */
     priority_queue<int> small;
     priority_queue<int, vector<int>, greater<int> > big;
     int n;
     MedianFinder() {
         n = 0;
     }
   
     void addNum(int num) {
         if (small.empty()){ small.push(num); n++; return ; }
         if (num<=small.top()) { small.push(num), n++; }
         else { big.push(num), n++;}
         if (small.size() - big.size() == 2){ big.push(small.top()), small.pop();}
         if (big.size() - small.size() == 2){ small.push(big.top()), big.pop();}
     }
   
     double findMedian() {
         if (n % 2){
             if (small.size()>big.size()) return small.top();
             return big.top();
         } else {
             return ((long long)small.top() + big.top()) * 0.5;
         }
     }
 };
 
 /**
  * Your MedianFinder object will be instantiated and called as such:
  * MedianFinder* obj = new MedianFinder();
  * obj->addNum(num);
  * double param_2 = obj->findMedian();
  */
 
```
