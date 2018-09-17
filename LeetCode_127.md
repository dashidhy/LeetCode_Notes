# 157. Read N Characters Given Read4

Problem link: [157. Read N Characters Given Read4](https://leetcode.com/problems/read-n-characters-given-read4/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

So easy.

## Implementation

### C++ (beats 100%)
```C++
// Forward declaration of the read4 API.
int read4(char *buf);

class Solution {
public:
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    int read(char *buf, int n) {
        int c = 4, out = 0, i = 0;
        while(true) {
            c = read4(&buf[i]);
            out += c; if(out > n) return n;
            if(c < 4) break;
            i += 4;
        }
        return out;
    }
};
```