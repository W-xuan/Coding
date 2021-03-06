#### [77. 组合](https://leetcode-cn.com/problems/combinations/)

给定两个整数 `n` 和 `k`，返回范围 `[1, n]` 中所有可能的 `k` 个数的组合。

你可以按 **任何顺序** 返回答案。

 

**示例 1：**

```
输入：n = 4, k = 2
输出：
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**示例 2：**

```
输入：n = 1, k = 1
输出：[[1]]
```

 ```C++
class Solution {
public:
vector<vector<int>> result;
    vector<vector<int>> combine(int n, int k) {
        vector<int> path;
        backtrack(n, k, 1, path);
        return result;
    }
    void backtrack(int n, int k, int step, vector<int>& path) {
        if (path.size() == k) {
            result.push_back(path);
            return;
        }
        if (step == n + 1) {
            return;
        }
        backtrack(n, k, step + 1, path);
        path.push_back(step);
        backtrack(n, k, step + 1, path);
        path.pop_back();
    }
};
 ```

