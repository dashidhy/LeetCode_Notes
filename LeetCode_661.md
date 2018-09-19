# 661. Image Smoother

Problem link: [661. Image Smoother](https://leetcode.com/problems/image-smoother/description/)

* Level: [Easy](https://leetcode.com/problemset/all/?difficulty=Easy)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Seems that we can't do it in-place.

## Implementation

### C++ (beats 98.29%)
```C++
class Solution {
public:
    vector<vector<int>> imageSmoother(vector<vector<int>>& board) {
        if(board.size() == 0 || board.size() * board[0].size() < 2) return board;
        int r = board.size() - 1, c = board[0].size() - 1;
        vector<vector<int>> board_o(board);
        int i, j;
        if(c == 0) {//only one colunm
            for(i = 0; i < r; ++i) {
                board_o[i][0] += board[i + 1][0];
                board_o[i + 1][0] += board[i][0];
                board_o[i][0] /= (i == 0)? 2:3;
            }
            board_o[r][0] /= 2;
            return board_o;
        }
        for(i = 0; i < r; ++i) {
            // first col
            board_o[i][0] += board[i][1] + board[i + 1][1] + board[i + 1][0];
            board_o[i][1] += board[i][0];
            board_o[i + 1][1] += board[i][0];
            board_o[i + 1][0] += board[i][0];
            board_o[i][0] /= (i == 0)? 4:6;
            // middle col
            for(j = 1; j < c; ++j) {
                board_o[i][j] += board[i][j + 1] + board[i + 1][j + 1] + board[i + 1][j] + board[i + 1][j - 1];
                board_o[i][j + 1] += board[i][j];
                board_o[i + 1][j + 1] += board[i][j];
                board_o[i + 1][j] += board[i][j];
                board_o[i + 1][j - 1] += board[i][j];
                board_o[i][j] /= (i == 0)? 6:9;
            }
            // last col
            board_o[i][c] += board[i + 1][c] + board[i + 1][c - 1];
            board_o[i + 1][c] += board[i][c];
            board_o[i + 1][c - 1] += board[i][c];
            board_o[i][c] /= (i == 0)? 4:6;
        }
        // last row
        for(j = 0; j < c; ++j) {
            board_o[r][j] += board[r][j + 1];
            board_o[r][j + 1] += board[r][j];
            board_o[r][j] /= (j == 0)? ((r == 0)? 2:4):((r == 0)? 3:6);
        }
        board_o[r][c] /= (r == 0)? 2:4;
        return board_o;
    }
};
```