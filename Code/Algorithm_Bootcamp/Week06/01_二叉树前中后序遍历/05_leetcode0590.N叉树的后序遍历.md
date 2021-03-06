#### [590. N 叉树的后序遍历](https://leetcode-cn.com/problems/n-ary-tree-postorder-traversal/)

给定一个 N 叉树，返回其节点值的 **后序遍历** 。

N 叉树 在输入中按层序遍历进行序列化表示，每组子节点由空值 `null` 分隔（请参见示例）。

 

**进阶：**

递归法很简单，你可以使用迭代法完成此题吗?

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
输入：root = [1,null,3,2,4,null,5,6]
输出：[5,6,3,2,4,1]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[2,6,14,11,7,3,12,8,4,13,9,10,5,1]
```

 **C++**

```c++
class Solution {
public:
    vector<int> postorder(Node* root) {
        if (!root) return {};
        vector<int> res;
        stack<Node*> stk;
        stk.push(root);
        while (!stk.empty()) {
            Node* node = stk.top();
            if (node == nullptr) {
                stk.pop();
                res.push_back(stk.top()->val);
                stk.pop();
            } else {
                stk.push(nullptr);
                for (int i = node->children.size() - 1; i >= 0; i -- )  {
                    if (node->children[i]) 
                    stk.push(node->children[i]);
                }
            }
        }
        return res;
    }
};
```

