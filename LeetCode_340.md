# 340. Longest Substring with At Most K Distinct Characters

Problem link: [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

We need to record and update the number of times that a character appears in the current substring. A hash table is the best solution.

### Best complexity

Time: O(n). Extra space: O(1).

### Key variables:

* **int** *head* ---- A pointer points to the first charactor of the current substring.
* **int** *tail* ---- A pointer points to the last charactor of the current substring.
* **int** *count* ---- A counter counts the number of distinct characters of the current substring.
* **int** *max* ---- Records the length of the longest substring.
* **int[]** *hash* ---- A hash table records the number of times a character appears in the current substring.

### Process:

1. While *count <= k*, move *tail*, and then update *hash* and *count*.
2. Update *max*.
3. While *count > k* and *head < tail*, update *hash* and *count*, and then move *head*.
4. Repeat from 1 until *tail* reaches the end.
5. Return *max*.

### Corner cases 

In general:

* *k == 0*.
* No answer (should return the length of *s*)

Algorithm:

* Maximum appears at the end of the string.

## Implementation

### Java (beats 100%)
```Java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (k == 0) return 0;
        
        char[] s_array = s.toCharArray();
        int head = 0, tail = 0, count = 0, s_length = s.length();
        char c;
        int max = 0, clength = 0;
        int[] hash = new int[128];
        
        while (tail < s_length) {
            c = s_array[tail];
            if (hash[c] == 0) {
                ++count;
            }
            ++hash[c];
            if (count > k) {
                clength = tail - head;
                if (clength > max) max = clength;
                while (head < tail && count > k) {
                    c = s_array[head];
                    --hash[c];
                    if (hash[c] == 0) --count;
                    ++head;
                }
            }
            ++tail;            
        }
        
        // Fix two corner cases with a single implementation
        clength = tail - head;
        if (clength > max) max = clength;
        
        return max;
    }
}
```