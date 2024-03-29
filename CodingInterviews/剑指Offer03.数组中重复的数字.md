#### [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

```
输入：[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

```c++
哈希表
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        unordered_map<int, bool> umap;
        for (int i = 0; i < nums.size(); i++) {
            if (umap[nums[i]]) return nums[i];
            umap[nums[i]] = true;
        }
        return -1;
    }
};
```

```c++
比较难想到的解法，因为数字都在0~n-1 而一共有n个，所以可以通过将数字放到对应坐标上，一旦发现数字与对应坐标不一致，即找到重复的数字
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        if (nums.empty()) return -1;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] < 0 || nums[i] > (nums.size() - 1)) return -1;
            while(nums[i] != i) {
                if (nums[i] == nums[nums[i]]) return nums[i];
                swap(nums[i], nums[nums[i]]);
            }
        }
        return -1;
    }
};
```
