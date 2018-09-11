# 683. K Empty Slots

Problem link: [683. K Empty Slots](https://leetcode.com/problems/k-empty-slots/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

*flowers* maps *day i -> slot x*. This mapping is hard to handle, so we should think about inversing the mapping to *slot x -> day i*. Traverse *flower* to inverse the mapping and we get *slots*, then we transfor the problem to a typical parttern matching problem. Inspired by KMP algorithm, we should try to move the parttern array as fast as possible to obtain an O(n) complexity.

## Best complexity

Time: O(n). Extra space: O(1);

## Implementation

### C++ (beats 98.16%)
```C++
class Solution {
public:
    int kEmptySlots(vector<int>& flowers, int k) {
        
        int N = flowers.size();
        
        // inverse the mapping
        vector<int> slots(N);
        int l, r, i, min = -1, max = 0;
        for(l = 0; l < N; ++l) {
            slots[flowers[l] - 1] = l + 1;
        }
        
        l = 0;
        while(l + k + 1 < N) {
            r = l + k + 1;
            for(i = l + 1; i < r; ++i) {
                if(slots[i] < slots[r]) {
                    l = i;
                    break;
                }
                else if(slots[i] < slots[l]) {
                    l = i + 1;
                    break;
                }
            }
            if(i == r) {
                max = (slots[l] > slots[r])? slots[l]:slots[r];
                min = (max < min || min == -1)? max:min;
                l = r;
            }
        }
        
        return min;
        
    }
};
```