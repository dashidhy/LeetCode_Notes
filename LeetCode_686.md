# 686. Repeated String Match

Problem link: [686. Repeated String Match](https://leetcode.com/problems/repeated-string-match/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Review the [KMP algorithm](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm) and the [Boyer-Moore algorithm](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string-search_algorithm).

## Implementation

### C++ (beats 99.01%)
```C++
class Solution {
public:
    int repeatedStringMatch(string A, string B) {
        int size_A = A.size(), size_B = B.size();
        int count = 1;
        string S = A;
        while(size_A * count < size_B) {
            ++count;
            S += A;
        }
        if(KMP(B, S)) return count;
        if(KMP(B, S + A)) return count + 1;
        return -1;
    }
    
    bool KMP(string a, string b) { // is a in b
        int size_a = a.size();
        int size_b = b.size();
        int max_a[size_a];
        
        max_a[0] = 0;
        int i = 1, j = 0;
        
        while(i < size_a) {
            if(a[i] == a[j]) max_a[i++] = ++j;
            else if(j > 0) j = max_a[j - 1];
            else max_a[i++] = 0;
        }
        
        i = 0; j = 0;
        while(i < size_b) {
            if(b[i] != a[j]) {
                if(j == 0) ++i;
                else j = max_a[j - 1];
            }
            else {
                if(j == size_a - 1) return true;
                ++i; ++j;
            }
        }
        return false;
    }
};
```