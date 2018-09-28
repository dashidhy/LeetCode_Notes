# 487. Max Consecutive Ones II

Problem link: [487. Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Save the number of last consecutive 1s (including 0 size 1s).

## Implementation

### C++ (beats 99.09%)
```C++
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int N = nums.size();
        int count = 0, count_l = 1, max = 0;
        for(int i = 0; i < N; ++i) {
            if(nums[i]) {
                ++count;
                ++count_l;
            }
            else {
                if(count > max) max = count;
                count = count_l;
                count_l = 1;
            }
        }
        return (count > max)? count:max;
    }
};
```