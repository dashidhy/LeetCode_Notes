# 179. Largest Number

Problem link: [179. Largest Number](https://leetcode.com/problems/largest-number/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)

## Hints

### Intuition

This is actually a math problem. The key is that when a-b > b-a then a must precede b in the final sequence. Proof of this conclusion is not that obvious. Briefly, if there exists some c which should be insert between a and b, it must be a-c-b, not b-c-a, otherwise c-a-b or a-b-c will be larger (this can be proved by digit-by-digit comparison).

## Implementation

### C++ (beats 99.85%)
```C++
class Solution {
public:
    string largestNumber(vector<int>& nums) {
        int N = nums.size();
        vector<string> nums_string(N);
        for(int i = 0; i < N; ++i) {
            nums_string[i] = to_string(nums[i]);
        }
        sort(nums_string.begin(), nums_string.end(), Solution::myfunction);
        string out = "";
        for(int i = 0; i < N; ++i) {
            out += nums_string[i];
        }
        return (out[0] == '0')? "0":out;
    }
    
    static bool myfunction(string a, string b) {
        string ab = a + b, ba = b + a;
        return ab > ba;
    }
};
```