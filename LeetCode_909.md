# 909. Snakes and Ladders

Problem link: [909. Snakes and Ladders](https://leetcode.com/contest/weekly-contest-103/problems/snakes-and-ladders/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Weekly Contest 103](https://leetcode.com/contest/weekly-contest-103)

## Hints 

### Intuition

If you are proficient in the BFS and the DFS of graphs, this problem is not that hard. This problem can be solved by both BFS and DFS, while BFS will return the minimum faster.

## Implementation

### DFS: C++
```C++
class Solution {
public:
    int snakesAndLadders(vector<vector<int>>& board) {
        int N = board.size();
        vector<int> list(N * N);
        vector<int> mins(N * N, -1);
        int i, j;
        for(i = 0; i < N; ++i) {
            for(j = 0; j < N; ++j) {
                if(i % 2 == 0) list[i * N + j] = board[N - 1 - i][j] - 1;
                else list[i * N + N - j - 1] = board[N - 1 - i][j] - 1;
            }
        }
        recur(list, mins, 0, 0, N * N - 1);
        return mins[N * N - 1];
    }
    
    void recur(vector<int> &board, vector<int> &mins, int cur, int cur_s, int M) {
        if(mins[cur] != -1 && mins[cur] <= cur_s) return; 
        if(mins[cur] == -1 || cur_s < mins[cur]) mins[cur] = cur_s;
        if(cur == M) return;
        for(int i = cur + 1; i <= cur + 6 && i <= M; ++i) {
            if(board[i] >= 0) recur(board, mins, board[i], cur_s + 1, M);
            else recur(board, mins, i, cur_s + 1, M);
        }
        return;
    }
};
```

### BFS: Python (copy from [lee215](https://leetcode.com/problems/snakes-and-ladders/discuss/173378/Diagram-and-BFS), pretty delicate code)

```Python
class Solution:
    def snakesAndLadders(self, board):
        n = len(board)
        need = {1: 0}
        bfs = [1]
        for x in bfs:
            for i in range(x + 1, x + 7):
                a, b = int((i - 1) / n), (i - 1) % n
                nxt = board[~a][b if a % 2 == 0 else ~b]
                if nxt > 0: i = nxt
                if i == n * n: return need[x] + 1
                if i not in need:
                    need[i] = need[x] + 1
                    bfs.append(i)
        return -1 
```

### BFS: C++
```C++
class Solution {
public:
    int snakesAndLadders(vector<vector<int>>& board) {
        int N = board.size();
        vector<int> list(N * N);
        vector<int> mins(N * N, -1);
        mins[0] = 0;
        queue<int> bfs;
        int i, j;
        for(i = 0; i < N; ++i) {
            for(j = 0; j < N; ++j) {
                if(i % 2 == 0) list[i * N + j] = board[N - 1 - i][j] - 1;
                else list[i * N + N - j - 1] = board[N - 1 - i][j] - 1;
            }
        }
        bfs.push(0);
        while(bfs.size() > 0) {
            i = bfs.front(); bfs.pop();
            for(j = i + 1; j < i + 7 && i < N * N; ++j) {
                int t = (list[j] >= 0)? list[j]:j;
                if(t == N * N - 1) return mins[i] + 1;
                if(mins[t] == -1) {mins[t] = mins[i] + 1; bfs.push(t);}
            }
        }
        return -1;
    }
};
```