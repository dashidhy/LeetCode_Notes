# 425. Word Squares

Problem link: [425. Word Squares](https://leetcode.com/problems/word-squares/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Use the prefix of the word as key for fast search.

## Implementation

### Python (beats 91%)
```Python
class Solution:
    
    def wordSquares(self, words):
        """
        :type words: List[str]
        :rtype: List[List[str]]
        """
        self.N = len(words[0])
        self.pref_dict = collections.defaultdict(list)
        self.squares = []
        
        # build the prefix dictionary
        for w in words:
            for i in range(1, self.N):
                self.pref_dict[w[:i]].append(w)
        
        # build squares by recursion
        for w in words:
            self.build_square([w])
            
        return self.squares
        
    def build_square(self, sq):
        n = len(sq)
        if n == self.N:
            self.squares.append(sq)
            return
        
        new_pref = ""
        for i in range(n):
            new_pref += sq[i][n]
            
        for word in self.pref_dict[new_pref]:
            self.build_square(sq + [word])
            
        return
```