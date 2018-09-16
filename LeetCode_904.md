# 904. Fruit Into Baskets

Problem link: [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Weekly Contest 102](https://leetcode.com/contest/weekly-contest-102)

## Hints 

### Intuition

A "K = 2" subcase of [LC340](https://github.com/dashidhy/LeetCode_Notes/blob/master/LeetCode_340.md).

## Implementation

### C++
```C++
class Solution {
public:
    int totalFruit(vector<int>& tree) {
        int tree_size = tree.size();
        int count = 0, c;
        int head = 0, tail = 0, clength = 0, max = 0;
        int hash[tree_size] = {0};
        while(tail < tree_size) {
            c = tree[tail];
            if(hash[c]++ == 0) ++count;
            
            if(count > 2) {
                clength = tail - head;
                if(clength > max) max = clength;
                while(head < tail && count > 2) {
                    c = tree[head++];
                    if(--hash[c] == 0) --count;
                }
            }
            ++tail;
        }
        clength = tail - head;
        if(clength > max) max = clength;
        return max;
    }
};
```