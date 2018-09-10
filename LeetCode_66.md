# 66. Plus One

Problem link: [66. Plus One](https://leetcode.com/problems/plus-one/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Easy.

### Best complexity

Time: O(n). Extra space: O(1).

### Corner cases 

In general:

* Numbers like 99999.

## Implementation

### C++ (beats 100%)
```C++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        for(int i = digits.size() - 1; i >= 0; --i) {
            digits[i] += 1;
            if(digits[i] == 10) 
                digits[i] = 0;
            else break;
        }
        if(digits[0] == 0) {
            digits[0] = 1;
            digits.push_back(0);
        }
        return digits;
    }
};
```