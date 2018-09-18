# 349. Intersection of Two Arrays

Problem link: [349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

You can do it in one line with python set and list operations.

## Implementation

### Python3 (beats 100%)
```Python
class Solution:
    def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        
        return list(set(nums1) & set(nums2))
```