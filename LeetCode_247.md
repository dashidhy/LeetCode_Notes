# 247. Strobogrammatic Number II

Problem link: [247. Strobogrammatic Number II](https://leetcode.com/problems/strobogrammatic-number-ii/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

So easy.

## Implementation

### Python (beats 98%)
```Python
class Solution:
    
    def findStrobogrammatic(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        
        self.out = []
        if n == 1:
            self.out = ['0', '1', '8']
        elif n > 1:
            if n % 2 == 1:
                self.build_s('0', n)
                self.build_s('1', n)
                self.build_s('8', n)
            else:
                self.build_s('', n)
        return self.out
        
    def build_s(self, core, n):
        if len(core) + 2 == n:
            self.out += ['1' + core + '1', '6' + core + '9', '8' + core + '8', '9' + core + '6']
            return
        self.build_s('0' + core + '0', n)
        self.build_s('1' + core + '1', n)
        self.build_s('6' + core + '9', n)
        self.build_s('8' + core + '8', n)
        self.build_s('9' + core + '6', n)
        return
```