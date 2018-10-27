# 918. Maximum Sum Circular Subarray

Problem link: [918. Maximum Sum Circular Subarray](https://leetcode.com/contest/weekly-contest-105/problems/maximum-sum-circular-subarray/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Weekly Contest 105](https://leetcode.com/contest/weekly-contest-105)

## Hints

### Intuition

The circular array is not a big deal, because we can just find the minimum subarray and minus it from the total sum then compare it with the maximun subarray. The most important problem is how to find the largest (or smallest) subarray from the whole array.

Take the largest subarray as the example. Think about the a property of the largest subarray: any prefix of the subarray must larger than zero, otherwise drop the prefix will make it larger. This property gives us the idea of our algorithm. From the head of the array, we enlarge our subarray if the sum of it larger than zero, otherwise we drop it and restart from the next element.

## Implementation

### Python (beats 99%)
```Python
class Solution:
    def maxSubarraySumCircular(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        curMax = 0
        curMin = 0
        MaxSum = A[0]
        MinSum = A[0]
        total = 0;
        for a in A:
            curMax = max(curMax + a, a)
            MaxSum = max(curMax, MaxSum)
            curMin = min(curMin + a, a)
            MinSum = min(curMin, MinSum)
            total += a
        
        if total == MinSum: 
            return MaxSum
        return max(total - MinSum, MaxSum)
            
```