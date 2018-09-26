# 270. Closest Binary Search Tree Value

Problem link: [270. Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Super easy. The smallest node larger than *target* is the nearest left turning point on the route from the root of the tree to the place where the *target* should be insert, and the largest point smaller is the nearest right turning point.

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
    int closestValue(TreeNode* root, double target) {
        int *left = NULL, *right = NULL;
        TreeNode *point = root;
        while(point) {
            if(target > point->val) {
                right = &(point->val);
                point = point->right;
            }
            else {
                left = &(point->val);
                point = point->left;
            }
        }
        if(left == NULL) return *right;
        if(right == NULL) return *left;
        return ((double) *left - target < target - (double) *right)? *left:*right;
    }
};
```