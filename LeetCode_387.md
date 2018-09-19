# 387. First Unique Character in a String

Problem link: [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Basic hash map.

## Implementation

### C++ (beats 100%)
```C++
class Solution {
public:
    int firstUniqChar(string s) {
        int hash[26] = {0};
        int N = s.size();
        for(char c : s) ++hash[c - 'a'];
        for(int i = 0; i < N; ++i) if(hash[s[i] - 'a'] == 1) return i;
        return -1;
    }
};
```