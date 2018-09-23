# 908. Smallest Range I

Problem link: [908. Smallest Range I](https://leetcode.com/contest/weekly-contest-103/problems/smallest-range-i/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Weekly Contest 103](https://leetcode.com/contest/weekly-contest-103)

## Hints 

### Intuition

Easy one.

## Implementation

### C++
```C++
class Solution {
public:
    int smallestRangeI(vector<int>& A, int k) {
        int N = A.size();
        if(N < 2) return 0;
        int min = A[0], max = A[0];
        for(int i = 1; i < N; ++i) {
            if(min > A[i]) min = A[i];
            if(max < A[i]) max = A[i];
        }
        int out = max - min - 2 * k;
        return (out < 0)? 0:out;
    }
};
```