# 687. Longest Univalue Path

Problem link: [687. Longest Univalue Path](https://leetcode.com/problems/longest-univalue-path/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Basic [tree traversal algorithms](https://en.wikipedia.org/wiki/Tree_traversal). In this problem we use post-order tracersal in order to get information form both child nodes.

## Implementation

### C++ (beats 97.78%)
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
    int max_path = 0;
    
    int longestUnivaluePath(TreeNode* root) {
        postOrder(root);
        return max_path;
    }
    
    int postOrder(TreeNode* t) {
        if(!t) return 0;
        int max_l = postOrder(t->left), max_r = postOrder(t->right);
        max_l = (t->left && t->left->val == t->val) ? ++max_l:0;
        max_r = (t->right && t->right->val == t->val) ? ++max_r:0;
        max_path = max(max_path, max_l + max_r);
        return max(max_l, max_r);
    }
};
```