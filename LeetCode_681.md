# 681. Next Closest Time

Problem link: [681. Next Closest Time](https://leetcode.com/problems/next-closest-time/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Just enumerate all possible solutions.

## Implementation

### C++ (beats 100%)
```C++
class Solution {
public:
    string nextClosestTime(string time) {
        
        char hash[10] = {0};
        int i, j, k, l, min = 1441, difft = 0;
        int time1[4];
        string out = "00:00";
        vector<int> digits;
        hash[time[0] - '0'] = 1;
        hash[time[1] - '0'] = 1;
        hash[time[3] - '0'] = 1;
        hash[time[4] - '0'] = 1;
        
        int time2[4] = {time[0] - '0', time[1] - '0', time[3] - '0', time[4] - '0'};
        
        for(i = 0; i < 10; ++i) {
            if(hash[i] == 1) digits.push_back(i);
        }
        
        int size_digits = digits.size();
        
        for(i = 0; i < size_digits; ++i) {
            
            if(digits[i] > 2) continue;
            time1[0] = digits[i];
            
            for(j = 0; j < size_digits; ++j) {
                
                if(digits[j] > 5) continue;
                time1[2] = digits[j];
                
                for(k = 0; k < size_digits; ++k) {
                    
                    if(time1[0] == 2 && digits[k] > 3) continue;
                    time1[1] = digits[k];
                    
                    for(l = 0; l < size_digits; ++l) {
                        time1[3] = digits[l];
                        difft = ((time1[0] - time2[0]) * 10 + time1[1] - time2[1]) * 60 + ((time1[2] - time2[2]) * 10 + time1[3] - time2[3]);
                        if(difft <= 0) difft += 1440;
                        if(min > difft) {
                            min = difft;
                            out[0] = ((char) time1[0]) + '0';
                            out[1] = ((char) time1[1]) + '0';
                            out[3] = ((char) time1[2]) + '0';
                            out[4] = ((char) time1[3]) + '0';
                        }
                    }
                }
            }
        }
        
        return out;
        
    }
};
```