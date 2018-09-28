# 207. 98. Validate Binary Search Tree

Problem link: [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Basic DFS and propertiy of BST.

## Implementation

### Python (beats 99.96%)
```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.DFS(root, float('-inf'), float('inf'))
    
    def DFS(self, root, l, r):
        if root:
            return root.val > l and root.val < r and self.DFS(root.left, l, root.val) and self.DFS(root.right, root.val, r)
        else:
            return True
```