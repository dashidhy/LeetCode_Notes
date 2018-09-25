# 399. Evaluate Division

Problem link: [399. Evaluate Division](https://leetcode.com/problems/evaluate-division/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Basic BFS is sufficient to beat 100%. However, there is a follow-up question that how to speed up the search if the queries come in a infinite datastream that includes a lot of same query pairs? To optimize this porblem, add union-find step is better. Every time we check a indirect connected pair, we add the edge between the pair to the graph, then the next time we query the same pair it will be O(1) time.

## Implementation

### C++ (beats 100%)
```C++
class Solution {
    
public:
    vector<double> calcEquation(vector<pair<string, string>> equ, vector<double>& val, vector<pair<string, string>> que) {
        unordered_map<string, vector<pair<string, double>>> gra;
        int N_e = equ.size(), N_q = que.size();
        int i;
        // build graph
        for(i = 0; i < N_e; ++i) {
            gra[equ[i].first].push_back({equ[i].second, val[i]});
            gra[equ[i].second].push_back({equ[i].first, 1.0 / val[i]});
        }
        vector<double> out;
        //BFS
        for(i = 0; i < N_q; ++i) {
            out.push_back(BFS(gra, que[i]));
        }
        return out;
    }
    
    double BFS(unordered_map<string, vector<pair<string, double>>> &gra, pair<string, string> &que) { //look up que in gra
        if(!gra.count(que.first) || !gra.count(que.second)) return -1.0;
        if(que.first == que.second) return 1.0;
        queue<string> bfs;
        unordered_map<string, double> out;
        bfs.push(que.first);
        out[que.first] = 1.0;
        while(!bfs.empty()) {
            string cur = bfs.front(); bfs.pop();
            for(int i = 0; i < gra[cur].size(); ++i) {
                if(gra[cur][i].first == que.second) return out[cur] * gra[cur][i].second;
                if(!out.count(gra[cur][i].first)) {
                    out[gra[cur][i].first] = out[cur] * gra[cur][i].second;
                    bfs.push(gra[cur][i].first);
                }
            }
        }
        return -1.0;
    }
    
};
```