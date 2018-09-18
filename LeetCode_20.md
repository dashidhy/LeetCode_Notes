# 20. Valid Parentheses

Problem link: [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Easy.

## Implementation

### Python3 (beats 99.72%)
```Python
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        left = {'(', '[', '{'}
        match = {('(', ')'), ('[', ']'), ('{', '}')}
        for c in s:
            if c in left:
                stack.append(c)
            else:
                if not stack or not (stack.pop(), c) in match:
                    return False
        return len(stack) == 0
```