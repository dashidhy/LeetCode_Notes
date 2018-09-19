# 485. Max Consecutive Ones

Problem link: [485. Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

So easy.

## Implementation

### C++ (beats 95.75%)
```C++
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int N = nums.size();
        int count = 0, max = 0, i = 0;
        while(i < N) {
            if(nums[i]) {
                ++count;
                ++i;
            }
            else {
                if(count > max) max = count;
                count = 0;
                while(i < N && !nums[i]) ++i;
            }
        }
        return (count > max)? count:max;
    }
};
```