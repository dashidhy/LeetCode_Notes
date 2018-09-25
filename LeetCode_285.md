# 285. Inorder Successor in BST

Problem link: [285. Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Easy one. Just make good use of BST's properties.

## Implementation

### C++ (beats 100%)
```C++
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
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        TreeNode *point = p;
        if(point->right) {
            point = point->right;
            while(point->left != NULL) point = point->left;
            return point;
        }
        point = root;
        TreeNode *nearest_left = NULL;
        while(point != p) {
            if(point->val > p->val) {
                nearest_left = point;
                point = point->left;
            }
            else point = point->right;
        }
        return nearest_left;
    }
};
```