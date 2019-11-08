# 125. Valid Palindrome

Problem link: [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

```C++
bool is_diff(char a, char b) {
        if(a == b || (a - 'A' == b - 'a') || (a - 'a' == b - 'A')) return false;
        return true;
    }
```

What's the problem of the code above? If you check the ASCII value, you will find '0' - 'A' = 'P' - 'a' = -17 !!

## Implementation

### C++ (beats 100%)
```C++
class Solution {
private:
    bool is_case(char c) {
        if((c >= '0' && c <= '9') || (c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z')) return false;
        return true;
    }
    
    bool is_diff(char a, char b) {
        if(a == b || (a - 'A' == b - 'a' && a - 'A' >= 0) || (a - 'a' == b - 'A' && a - 'a' >= 0)) return false;
        return true;
    }
public:
    bool isPalindrome(string s) {
        int head = 0, tail = s.size() - 1;
        while(head < tail) {
            if(is_case(s[head])) {++head; continue;}
            if(is_case(s[tail])) {--tail; continue;}
            if(is_diff(s[head++], s[tail--])) return false;
        }
        return true;
    }
};
```

### O(1) space complexity solution
The only thing that needs to be store is the number of the left parenthesis. The algorithms starts with counting the number of the left parenthesis while going through the array. When there is a right parenthesis, the counter decrease one and add one whenever there is a left parenthesis. The loop breaks when the counter is negative, which means there is an invalid right parenthesis. Eventually, when the counter is still positive in the end which means there are additional left parenthesis, the solution will return False and True otherwise when counter is equal to zero.
