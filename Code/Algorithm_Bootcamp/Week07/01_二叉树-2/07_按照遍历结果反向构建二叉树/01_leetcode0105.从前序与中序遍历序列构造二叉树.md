#### [105. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

给定一棵树的前序遍历 `preorder` 与中序遍历 `inorder`。请构造二叉树并返回其根节点。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**示例 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

 ### c++

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
private:
        TreeNode* traversal (vector<int>& inorder, int inorderBegin, int inorderEnd, vector<int>& preorder, int preorderBegin, int preorderEnd) {
        if (preorderBegin == preorderEnd) return NULL;

        int rootValue = preorder[preorderBegin]; 
        TreeNode* root = new TreeNode(rootValue);

        if (preorderEnd - preorderBegin == 1) return root;

        int iter = 0;
        while (inorder[iter] != rootValue) iter++;
        int leftInorderBegin = inorderBegin;
        int leftInorderEnd = iter;
        int rightInorderBegin = iter + 1;
        int rightInorderEnd = inorderEnd;

        int leftPreorderBegin =  preorderBegin + 1;
        int leftPreorderEnd = preorderBegin + 1 + iter - inorderBegin; 
        int rightPreorderBegin = preorderBegin + 1 + (iter - inorderBegin);
        int rightPreorderEnd = preorderEnd; 

        root->left = traversal(inorder, leftInorderBegin, leftInorderEnd,  preorder, leftPreorderBegin, leftPreorderEnd);
        root->right = traversal(inorder, rightInorderBegin, rightInorderEnd, preorder, rightPreorderBegin, rightPreorderEnd);

        return root;
    }

public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if (inorder.size() == 0 ) return NULL;
        return traversal(inorder, 0, inorder.size(), preorder, 0, preorder.size());
    }
};
```

### c

```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
struct TreeNode* getNewNode(int key) {
    struct TreeNode *p = (struct TreeNode *)malloc(sizeof(struct TreeNode));
    p->val = key;
    p->left = p->right = NULL;
    return p;
}

struct TreeNode* buildTree(int* preorder, int preorderSize, int* inorder, int inorderSize) {
    if(preorderSize == 0) return NULL;
    int key = preorder[0], n = preorderSize;
    struct TreeNode *root = getNewNode(key);
    int ind = 0;
    while(inorder[ind] != key) ++ind;
    root->left = buildTree(preorder + 1, ind, inorder, ind);
    root->right = buildTree(preorder + ind + 1, n - ind - 1, inorder + ind + 1, preorderSize);
    return root;
}
```
