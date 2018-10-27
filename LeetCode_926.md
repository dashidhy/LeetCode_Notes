# 926. Flip String to Monotone Increasing

Problem link: [926. Flip String to Monotone Increasing](https://leetcode.com/contest/weekly-contest-107/problems/flip-string-to-monotone-increasing/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Weekly Contest 107](https://leetcode.com/contest/weekly-contest-107)

## Hints

### Intuition

Typical DP problem. If s[n] == '1', monotonicity keeps unchanged, F(n) = F(n - 1). If s[n] == '0', we have two method to make the array monotone increasing: change the '0' to '1', or change all previous '1' to '0', so F(n) = min(F(n - 1) + 1, num_ones(n - 1)). 

## Implementation

### C++
```C++
class Solution {
public:
    int minFlipsMonoIncr(string S) {
        int out = 0, num_one = 0;
        for(char s : S) {
            if(s == '0') out = min(out + 1, num_one);
            else ++num_one;
        }
        return out;
    }
};
```