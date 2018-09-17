# 158. Read N Characters Given Read4 II - Call multiple times

Problem link: [158. Read N Characters Given Read4 II - Call multiple times](https://leetcode.com/problems/read-n-characters-given-read4-ii-call-multiple-times/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

The description of this problem is unclear and misleading. You should firstly figure out how *read4* works.

*read4* have a hidden file pointer which updates itself whenever it is called. So here comes a porblem that the file pointer is ahead of the position you should start to read. Thus, you should buffer the redundant characters and push them into *buf* when *read* is called again.

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
    char buffer[5];
    int len = 0;
    bool ifbuffer = false;
    
    int read(char *buf, int n) {
        int c, out = 0, i = 0;
        if(ifbuffer) {
            for(i = 0; i < len; ++i) buf[i] = buffer[i];
            out = len;
            ifbuffer = false;
        }
        while(out < n) {
            c = read4(&buf[i]);
            out += c; 
            if(c < 4) break;
            i += c;
        }
        if(out > n) {
            for(i = n; i < out; ++i) buffer[i - n] = buf[i];
            len = out - n;
            ifbuffer = true;
            return n;
        }
        return out;
    }
};
```