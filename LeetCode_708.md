# 708. Insert into a Cyclic Sorted List

Problem link: [708. Insert into a Cyclic Sorted List](https://leetcode.com/problems/insert-into-a-cyclic-sorted-list/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Easy problem. You just have to properly fix the corner cases that when you have to insert at head or tail.

## Implementation

### C++ (beats 100%)
```C++
/*  Definition for a Node.
class Node {
public:
    int val;
    Node* next;

    Node() {}

    Node(int _val, Node* _next) {
        val = _val;
        next = _next;
    }
}; */
class Solution {
public:
    Node* insert(Node* head, int Val) {
        Node* t_node = new Node(Val, NULL);
        t_node->next = t_node;
        if(!head) return t_node;
        Node* cur = head;
        while(true) {
        	// normal insert
            if(Val >= cur->val && Val <= cur->next->val) break;
            // head or tail
            if(cur->val >= cur->next->val && (Val >= cur->val || Val <= cur->next->val)) break;
            cur = cur->next;
        }
        t_node->next = cur->next;
        cur->next = t_node;
        return head;
    }
};
```