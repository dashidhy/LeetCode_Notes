# 283. Move Zeroes

Problem link: [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Do it in-place by swapping a non-zero number with the first 0.

## Implementation

### C++ (beats 100%)
```C++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int N = nums.size();
        int i, first_0 = -1;
        for(i = 0; i < N; ++i) {
            if(nums[i] && first_0 != -1) {
                nums[first_0++] = nums[i];
                nums[i] = 0;
            }
            else if(!nums[i] && first_0 == -1) first_0 = i;
        }
    }
};
```