# 41. First Missing Positive

Problem link: [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Notice that the first missing positive must be in 1 ~ N, where N is the length of the input array. If we put every number in [1, N] into its right position (*i* should be at *A[i - 1]*), then the first position which does not contain the right number is the missing one.

## Implementation

### C++ (beats 100%)
```C++
class Solution {
public:
    int firstMissingPositive(vector<int>& A) {
        int N = A.size(), i;
        for(i = 0; i < N; ++i) {
            while(A[i] > 0 && A[i] <= N && A[A[i] - 1] != A[i]) swap(A[i], A[A[i] - 1]);
        }
        for(i = 1; i <= N; ++i) {
            if(A[i - 1] != i) return i;
        }
        return i;
    }
};
```