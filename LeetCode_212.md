# 212. Word Search II

Problem link: [212. Word Search II](https://leetcode.com/problems/word-search-ii/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

If you only use DFS you will get time limit exceeded. Combined with Trie, you can travse the board only once and try to find as more words in the word array as you can.

### C++ (beats 99.69%)
```C++
class Solution {
private:
    struct TrieNode {
        TrieNode* next[26];
        int idx = -1; // idx >= 0: index in words; idx < 0: word non-exist (or visited)
        TrieNode() {
            for(int i = 0; i < 26; ++i) {
                next[i] = NULL;
            }
        }
    };
    void dfs(TrieNode *node, vector<vector<char>> &board, int i, int j, vector<string>& words, vector<string> &out) {
        if(node->idx != -1) { // find a word that has not visited
            out.push_back(words[node->idx]);
            node->idx = -1; // visited
        }
        
        if(i < 0 || j < 0 || i >= board.size() || j >= board[0].size()) return; // out of board
        char c = board[i][j];
        if(c && node->next[c - 'a']) {
            c -= 'a'; 
            board[i][j] = 0; // don't use again
            dfs(node->next[c], board, i + 1, j, words, out);
            dfs(node->next[c], board, i, j + 1, words, out);
            dfs(node->next[c], board, i - 1, j, words, out);
            dfs(node->next[c], board, i, j - 1, words, out);
            board[i][j] = c + 'a';
        }
        return;
    }
    
public:    
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        
        int num_r = board.size(), num_c = board[0].size(), num_w = words.size();
        
        // build the trie
        TrieNode *root = new TrieNode();
        for(int i = 0; i < num_w; ++i) {
            TrieNode *node = root;
            for(int j = 0; j < words[i].size(); ++j) {
                char c = words[i][j] - 'a';
                if(node->next[c] == NULL) node->next[c] = new TrieNode();
                node = node->next[c];
            }
            node->idx = i;
        }
        vector<string> out;
        for(int i = 0; i < num_r; ++i) {
            for(int j = 0; j < num_c; ++j) {
                dfs(root, board, i, j, words, out);
            }
        }
        return out;
    }
    
};
```