# 214. Shortest Palindrome

Problem link: [214. Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

The problem can be converted into finding the longest palindrome substring from the input's beginning. Recall the KMP algorithm, we can modify it on input *s* and it's reverse. However, there is a corner case that if *s* itself is a palindrome.

There are two ways to fix the corner case. We can firstly judge if *s* is a palindrome, if true, return. We can also create a new string *s_new = s + '#' + s_reverse* and then do KMP on *s_new*.

## Implementation

### C++ (beats 100%)
```C++
class Solution {
public:
    string shortestPalindrome(string s) {
        int N = s.length();
        if(N < 2) return s;
        int i = 0, j = N - 1;
        while(i < j) {
            if(s[i] != s[j]) break;
            ++i; --j;
        }
        if(i >= j) return s;
        int Next[N] = {0};
        string s_r = s;
        reverse(s_r.begin(), s_r.end());
        i = 1, j = 0;
        while(i < N) {
            if(s_r[i] == s[j]) Next[i++] = ++j;
            else if(j > 0) j = Next[j - 1];
            else Next[i++] = 0;
        }
        return s_r + s.substr(Next[N - 1], N);
    }
};
```