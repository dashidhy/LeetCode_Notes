# 906. Super Palindromes

Problem link: [906. Super Palindromes](https://leetcode.com/problems/super-palindromes/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Weekly Contest 102](https://leetcode.com/contest/weekly-contest-102)

## Hints 

### Intuition

* An integer can be used to generate two palindromes. For example, 1234 can generate 1234321 and 12344321.
* *int(L)* and *int(R)* are smaller than 10^18, so the square roots of target palindromes are no more than 10^9. Thus the integers used to generate the palindrome square roots are no more than 10^5.
* Try evey integer which less than 10^5 to generate a square root and test if it lead to a target palindrome. Break the loop when beyond the boundary.

## Implementation

### C++
```C++
typedef long long ll;
class Solution {
public:
    int superpalindromesInRange(string L, string R) {
        ll l = stoll(L), r = stoll(R);
        int out = 0;
        for(int i = 1; i < 100000; ++i) {
            int palin = i, t = i;
            //even palin
            while(t > 0) {
                palin = palin * 10 + t % 10;
                t /= 10;
            }
            ll palin_2 = (ll) palin * (ll) palin;
            if (palin_2 >= l && palin_2 <= r && is_P(palin_2)) ++out;
            //odd palin
            palin = i/10, t = i;
            while(t > 0) {
                palin = palin * 10 + t % 10;
                t /= 10;
            }
            palin_2 = (ll) palin * (ll) palin; if(palin_2 > r) break;
            if (palin_2 >= l && palin_2 <= r && is_P(palin_2)) ++out;
        }
        return out;
    }
    
    bool is_P(ll palin) {
        string p = to_string(palin);
        int head = 0, tail = p.length() - 1;
        while(head < tail) if(p[head++] != p[tail--]) return false;
        return true;
    }
    
};
```
