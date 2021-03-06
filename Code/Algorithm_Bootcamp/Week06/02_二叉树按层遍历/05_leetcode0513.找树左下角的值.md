#### [513. 找树左下角的值](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)

给定一个二叉树的 **根节点** `root`，请找出该二叉树的 **最底层 最左边** 节点的值。

假设二叉树中至少有一个节点。

**示例 1:**

![img](https://assets.leetcode.com/uploads/2020/12/14/tree1.jpg)

```
输入: root = [2,1,3]
输出: 1
```

**示例 2:**

![img](https://assets.leetcode.com/uploads/2020/12/14/tree2.jpg)

```
输入: [1,2,3,4,null,5,6,null,null,7]
输出: 7
```

**C++**

```C++
class Solution {
public:
    int ans, maxd = 0;

    int findBottomLeftValue(TreeNode* root) {
        dfs(root, 1);
        return ans;
    }

    void dfs(TreeNode* root, int d) {
        if (!root) return;
        if (d > maxd) {
            maxd = d;
            ans = root->val;
        }
        dfs(root->left, d + 1), dfs(root->right, d + 1);
    }
};
```
