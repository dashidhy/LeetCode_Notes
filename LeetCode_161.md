# 161. One Edit Distance

Problem link: [161. One Edit Distance](https://leetcode.com/problems/one-edit-distance/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

This problem is not so easy because there are some corner cases that you should deal with. Judge from the size of the strings that if it is "insert", "delete" or "replace" and then traverse the strings will help.

### Corner Cases

* String *s* and *t* are same, should return *false*.
* Null strings

## Implementation

### C++ (beats 100%)
```C++
class Solution {
public:
    bool isOneEditDistance(string s, string t) {
        int s_size = s.size(), t_size = t.size();
        int dif = s_size - t_size;
        if(dif > 1 || dif < -1) return false;
        int i = 0, j = 0;
        bool diff;
        if(dif == -1) { // insert
            diff = false;
            while(i < s_size && j < t_size) {
                if(s[i++] != t[j++]) {
                    if(diff) return false;
                    diff = true;
                    if(s[--i] != t[j]) return false;
                } 
            }
            return true;
        }
        if(dif == 1) { // delete
            diff = false;
            while(i < s_size && j < t_size) {
                if(s[i++] != t[j++]) {
                    if(diff) return false;
                    diff = true;
                    if(s[i] != t[--j]) return false;
                } 
            }
            return true;
        }
        if(dif == 0) { // replace
            diff = false;
            while(i < s_size && j < t_size) {
                if(s[i++] != t[j++]) {
                    if(diff) return false;
                    diff = true;
                } 
            }
            return (diff)? true:false;
        }
    }
};
```