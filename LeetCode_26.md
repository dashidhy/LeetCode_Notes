# 26. Remove Duplicates from Sorted Array

Problem link: [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Similar to [LC283](https://github.com/dashidhy/LeetCode_Notes/blob/master/LeetCode_283.md).

## Implementation

### C++ (beats 99.06%)
```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int N = nums.size(); if(N < 2) return N;
        int first_swap = 0;
        for(int i = 1; i < N; ++i) {
            if(nums[i] != nums[first_swap]) nums[++first_swap] = nums[i];
        }
        return ++first_swap;
    }
};
```