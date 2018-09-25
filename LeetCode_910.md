# 910. Smallest Range II

Problem link: [910. Smallest Range II](https://leetcode.com/problems/smallest-range-ii/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Weekly Contest 103](https://leetcode.com/contest/weekly-contest-103)

## Hints 

### Intuition

This problem is actually math. Notice that to reach the best result, +K should always present before -K (to make sure the operation will enlarge the interval as small as possiable).

## Implementation

### C++
```C++
class Solution {
public:
    int smallestRangeII(vector<int>& A, int k) {
        int N = A.size();
        if(N < 2) return 0;
        sort(A.begin(), A.end());
        int max_m = A[N - 1] - k, min_p = A[0] + k, out = A[N - 1] - A[0] + 2 * k;
        for(int i = 0; i < N - 1; ++i) {
            int max = (max_m > A[i] + k)? max_m:A[i] + k;
            int min = (min_p < A[i + 1] - k)? min_p:A[i + 1] - k;
            if(out > max - min) out = max - min;
        }
        return (out > A[N - 1] - A[0])? A[N - 1] - A[0]:out; // all plus or all minus
    }
};
```