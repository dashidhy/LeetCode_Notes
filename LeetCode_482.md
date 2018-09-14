# 482. License Key Formatting

Problem link: [482. License Key Formatting](https://leetcode.com/problems/license-key-formatting/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Just traverse the input string .

### Corner cases

In general:

* The number of alphanumeric characters is divisible by K.
* The leading characters are '-'.

## Implementation

### C++ (beats 98.68%)
```C++
class Solution {
public:
    string licenseKeyFormatting(string S, int K) {
        int size_S = S.length();
        int i, count = 0;
        string out;
        for(i = 0; i < size_S; ++i) {
            if(S[i] != '-') {
                if(S[i] >= 'a' && S[i] <= 'z') {
                    S[i] += 'A' - 'a'; 
                }
                ++count;
            }
        }
        if(count % K == 0) {
            for(i = 0; i < size_S; ++i) {
                if(S[i] != '-') break;
            }
            out.push_back(S[i]);
            --count;
            ++i;
        }
        else i = 0;
        for(; i < size_S; ++i) {
            if(S[i] != '-') {
                if(count % K == 0) out.push_back('-');
                out.push_back(S[i]);
                --count;
            }
        }
        return out;
    }
};
```