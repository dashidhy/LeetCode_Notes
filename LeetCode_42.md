# 42. Trapping Rain Water

Problem link: [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

A bar can hold water as long as there are higher bars on its both sides.

### Best complexity

Time: O(n). Extra space: O(1).

### Key variables:

* **int** *l* ---- A pointer points to the left side.
* **int** *r* ---- A pointer points to the right side.
* **int** *max_l* ---- Records the maximum left height.
* **int** *max_r* ---- Records the maximum right height.
* **int** *out* ---- Value for return.

### Process:

1. Compare *height[l]* and *height[r]*. For example,  *height[l] < height[r]*.
2. If *height[l] >= max_l*, update *max_l*. Else, *height[l]* can hold water because it's between and shorter than *max_l* and *height[r]*, so *out += max_l - height[l]*. (*r* is similar)
3. Move *l* (*r*).
4. Repeat from 1 until *l* meets *r*.
5. Return *out*.

### Corner cases 

In general:

* *height.size() == 0*.

## Implementation

### c++ (beats 100%)
```C++
class Solution {
public:
    int trap(vector<int>& height) {
        if(height.size() == 0) return 0;
        int l, max_l, r, max_r, out = 0;
        l = 0;
        r = height.size() - 1;
        max_l = height[l];
        max_r = height[r];
        while(l < r) {
            if(height[l] < height[r]) {
                if(height[l] >= max_l) 
                    max_l = height[l];
                else
                    out += max_l - height[l];
                ++l;
            }
            else {
                if(height[r] >= max_r) 
                    max_r = height[r];
                else
                    out += max_r - height[r];
                --r;
            }
        }
        return out;
    }
};
```