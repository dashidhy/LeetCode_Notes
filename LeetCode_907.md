# 907. Sum of Subarray Minimums

Problem link: [907. Sum of Subarray Minimums](https://leetcode.com/problems/sum-of-subarray-minimums/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Weekly Contest 102](https://leetcode.com/contest/weekly-contest-102)

## Hints 

### Intuition

Easy to come up with an $O(n^2)$ method. If you want to do it in $O(n)$, some math properties will help you optimize the algorithm.

Think about how many times a number will be counted in the process. *A[i]* will be counted *(r - i) *\**(i - l)* times where *r* is the index of the first element smaller than *A[i]* on its right side, and *l* is the index of the first element smaller than *A[i]* on its left side.

### Algorithm

Use a *stack* to archive indexes of *A*. The stack suffices that *A[stack[k - 1]]* is the first element smaller than *A[stack[k]]* on *A[stack[k]]* 's left side. 

Use a pointer *i* to traverse *A*. if *A[i] < A[stack[top]]*, we find a possible right boundary (of *A[stack[top]]*, as least). Pop out *stack[top]* and calculate the increment until *A[i] > A[stack[top]]*, we find *A[i]* 's left boundary, then push *i* into *stack*.

You should remember to fix the corner cases that *i == 0* and *i == A.size()*.

## Implementation

### C++
```C++
class Solution {
public:
    int sumSubarrayMins(vector<int>& A) {
        int N = A.size();
        int stack[N], head = -1;
        int i, cur, out = 0;
        for(i = 0; i < N; ++i) {
            while(head >= 0 && A[i] < A[stack[head]]) { //stack[head] meets its right boundary
                cur = stack[head--];
                if(head < 0) out += A[cur] * (i - cur) * (cur + 1);
                else out += A[cur] * (i - cur) * (cur - stack[head]);
                out %= 1000000007;
            }
            stack[++head] = i;
        }
        while(head >= 0) {
            cur = stack[head--];
            if(head < 0) out += A[cur] * (i - cur) * (cur + 1);
            else out += A[cur] * (i - cur) * (cur - stack[head]);
            out %= 1000000007;     
        }
        return out;
    }
};
```
