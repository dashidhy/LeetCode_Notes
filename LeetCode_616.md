# 616. Add Bold Tag in String

Problem link: [616. Add Bold Tag in String](https://leetcode.com/problems/add-bold-tag-in-string/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Approach 1: Label

### Intuition

To deal with the overlapped substrings, we can just label the specific character if it is bold. Then, we detect the changes of labels to decide where to insert tags.

## Implementation

### C++ (beats 87.34%)
```C++
class Solution {
public:
    string addBoldTag(string s, vector<string>& dict) {
        int size_s = s.length();
        int size_dict = dict.size();
        int i;
        bool bold[size_s + 2] = {0};
        
        for(i = 0; i < size_dict; ++i) KMP(dict[i], s, bold);
        
        stringstream out;
        int start = 0;
        for(i = 0; i <= size_s; ++i) {
            if(bold[i] == false && bold[i + 1] == true) {
                out<<s.substr(start, i - start);
                start = i;
            }
            if(bold[i] == true && bold[i + 1] == false) {
                out<<"<b>"<<s.substr(start, i - start)<<"</b>";
                start = i;
            }
        }
        out<<s.substr(start, i - start);
        return out.str();
    }
    
    void KMP(string a, string b, bool bold[]) {
        int size_a = a.size();
        int size_b = b.size();
        int max_a[size_a];
        
        max_a[0] = 0;
        int i = 1, j = 0;
        
        while(i < size_a) {
            if(a[i] == a[j]) max_a[i++] = ++j;
            else if(j > 0) j = max_a[j - 1];
            else max_a[i++] = 0;
        }
        
        i = 0; j = 0;
        while(i < size_b) {
            if(b[i] != a[j]) {
                if(j == 0) ++i;
                else j = max_a[j - 1];
            }
            else {
                ++i;
                if(j == size_a - 1) { // match
                    j = max_a[j];
                    for(int k = i - size_a; k < i; ++k) {
                        bold[k + 1] = true;
                    }
                }
                else ++j;
            }
        }
    }
};
```

<br/>

## Approach 2: Stack

### Intuition

Use a stack to deal with tags matching. Little bit space consuming, but achieves roughly the same speed and it's a good paractice of stack operations.

## Implementation

### C++ (beats 87.34%)
```C++
class Solution {
public:
    string addBoldTag(string s, vector<string>& dict) {
        int size_s = s.length() + 1;
        int size_dict = dict.size();
        char insert_l[size_s] = {0}, insert_r[size_s] = {0};
        int i, count = 0, head = -1;
        int stack[size_s] = {0};
        
        for(i = 0; i < size_dict; ++i) KMP(dict[i], s, insert_l, insert_r);
        
        for(i = 0; i < size_s; ++i) {
            if(insert_l[i] > 0) stack[++head] = i;
            if(insert_r[i] > 0) {
                while(insert_r[i] > 1) {
                    --insert_r[i];
                    --insert_l[stack[head]];
                    if(insert_l[stack[head]] == 0) --head;
                }
                if(head > 0 || insert_l[stack[0]] > 1) {
                    --insert_r[i];
                    --insert_l[stack[head]];
                    if(insert_l[stack[head]] == 0) --head;
                }
                else --head;
            }
        }
        
        for(i = size_s - 1; i >= 0; --i) {
            if(insert_r[i] > 0) s.insert(i, "</b>");
            if(insert_l[i] > 0) s.insert(i, "<b>");
        }
        
        return s;
    }
    
    void KMP(string a, string b, char insert_l[], char insert_r[]) { // is a in b
        int size_a = a.size();
        int size_b = b.size();
        int max_a[size_a];
        
        max_a[0] = 0;
        int i = 1, j = 0;
        
        while(i < size_a) {
            if(a[i] == a[j]) max_a[i++] = ++j;
            else if(j > 0) j = max_a[j - 1];
            else max_a[i++] = 0;
        }
        
        i = 0; j = 0;
        while(i < size_b) {
            if(b[i] != a[j]) {
                if(j == 0) ++i;
                else j = max_a[j - 1];
            }
            else {
                ++i;
                if(j == size_a - 1) { // match
                    ++insert_l[i - size_a]; ++insert_r[i];
                    j = max_a[j];
                }
                else ++j;
            }
        }
    }
};
```