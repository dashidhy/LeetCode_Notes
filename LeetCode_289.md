# 289. Game of Life

Problem link: [289. Game of Life](https://leetcode.com/problems/plus-one/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

A fully in-place implementation is really tricky and tedious (and seems unnecessary). Since the data type is int, a positive number can represent "live", a negative numbers can represent "dead", and its absolute value archives the number of live cells around it (including itself). 

### Complexity Analysis

* Time: O(N), where N is the number of *board* 's elements.
* Extra space: O(1). *i*, *j*, *r*, and *c* are the only extra variables used.

## Implementation

### C++ (beats 100%)
```C++
class Solution {
public:
    void gameOfLife(vector<vector<int>>& board) {
        if(board.size() == 0 || board[0].size() == 0) return;
        int r = board.size() - 1, c = board[0].size() - 1;
        int i, j;
        if(c == 0) {//only one colunm
            for(i = 0; i < r; ++i) {
                if(board[i][0] > 0) {
                    if(board[i + 1][0] > 0) {
                        ++board[i + 1][0];
                        ++board[i][0];
                    }
                    else --board[i + 1][0];
                }
                else if(board[i + 1][0] > 0) --board[i][0];
                board[i][0] = (board[i][0] == 3)? 1:0;
            }
            board[r][0] = (board[i][0] == 3)? 1:0;
            return;
        }
        for(i = 0; i < r; ++i) {
            // first col
            if(board[i][0] > 0) {//live
                if(board[i][1] > 0) {
                    ++board[i][1];
                    ++board[i][0];
                } else --board[i][1];
                if(board[i + 1][1] > 0) {
                    ++board[i + 1][1];
                    ++board[i][0];
                } else --board[i + 1][1];
                if(board[i + 1][0] > 0) {
                    ++board[i + 1][0];
                    ++board[i][0];
                } else --board[i + 1][0];
            }
            else {//dead
                if(board[i][1] > 0) --board[i][0];
                if(board[i + 1][1] > 0) --board[i][0];
                if(board[i + 1][0] > 0) --board[i][0];
            }
            board[i][0] = (board[i][0] == -3 || board[i][0] == 3 || board[i][0] == 4)? 1:0;
            // middle col
            for(j = 1; j < c; ++j) {
                if(board[i][j] > 0) {
                    if(board[i][j + 1] > 0) {
                        ++board[i][j + 1];
                        ++board[i][j];
                    } else --board[i][j + 1];
                    if(board[i + 1][j + 1] > 0) {
                        ++board[i + 1][j + 1];
                        ++board[i][j];
                    } else --board[i + 1][j + 1];
                    if(board[i + 1][j] > 0) {
                        ++board[i + 1][j];
                        ++board[i][j];
                    } else --board[i + 1][j];
                    if(board[i + 1][j - 1] > 0) {
                        ++board[i + 1][j - 1];
                        ++board[i][j];
                    } else --board[i + 1][j - 1];
                }
                else {
                    if(board[i][j + 1] > 0) --board[i][j];
                    if(board[i + 1][j + 1] > 0) --board[i][j];
                    if(board[i + 1][j] > 0) --board[i][j];
                    if(board[i + 1][j - 1] > 0) --board[i][j];
                }
                board[i][j] = (board[i][j] == -3 || board[i][j] == 3 || board[i][j] == 4)? 1:0;
            }
            // last col
            if(board[i][c] > 0) {//live
                if(board[i + 1][c] > 0) {
                    ++board[i + 1][c];
                    ++board[i][c];
                } else --board[i + 1][c];
                if(board[i + 1][c - 1] > 0) {
                    ++board[i + 1][c - 1];
                    ++board[i][c];
                } else --board[i + 1][c - 1];
            }
            else {//dead
                if(board[i + 1][c] > 0) --board[i][c];
                if(board[i + 1][c - 1] > 0) --board[i][c];
            }
            board[i][c] = (board[i][c] == -3 || board[i][c] == 3 || board[i][c] == 4)? 1:0;
        }
        // last row
        for(j = 0; j < c; ++j) {
            if(board[r][j] > 0) {
                if(board[r][j + 1] > 0) {
                    ++board[r][j + 1];
                    ++board[r][j];
                } else --board[r][j + 1];
            }
            else if(board[r][j + 1] > 0) --board[r][j];
            board[r][j] = (board[r][j] == -3 || board[r][j] == 3 || board[r][j] == 4)? 1:0;
        }
        board[r][c] = (board[r][j] == -3 || board[r][j] == 3 || board[r][j] == 4)? 1:0;
        return;
    }
};
```