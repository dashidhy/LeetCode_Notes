# 23. Merge k Sorted Lists

Problem link: [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Best complexity is O(N\*log(k)), where N is the number of total nodes and k is the number of lists. There are two ways to reach the bext complexity. The first is merging the lists 2 by 2 until getting one list. The procedure will happens log_2(k) times and each time we merges N nodes. Note that it will be easier to code if you merge the head and tail pair each time instead of the adjacent pair.

The second way is totally different. It's easy to come up with an idea that each time we add the smallest head of the lists into the output then finally we will get the result. A naive way to do this is to traverse the heads of the lists to get the minimum, but in this way it will take k times to add one node so the final complexity is O(N\*k). A alternative and more advanced way is using a priority queue. Every time we pop the priority queue to add it to the output and insert the new one. The pop takes O(1) and the insert takes O(log(k)). 

## Implementation

### 2 by 2: C++ (beats 100%)

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
private:
    void merge2(ListNode* &tar, ListNode* &mer) { // merge mer to tar
        if(!mer) return;
        if(!tar) {tar = mer; return;}
        ListNode* t;
        if(mer->val < tar->val) { // first insert at head
            t = mer;
            mer = mer->next;
            t->next = tar;
            tar = t;
        }
        ListNode* _tar = tar, *_mer = mer;
        while(_mer) {
            while(_tar->next && _mer->val >= _tar->next->val) _tar = _tar->next;
            t = _mer;
            _mer = _mer->next;
            t->next = _tar->next;
            _tar->next = t;
            _tar = _tar->next;
        }
        return;
    }
    
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        int k = lists.size();
        if(k == 0) return NULL;
        while(k > 1) {
            int i = 0, j = k - 1;
            while(i < j) {
                merge2(lists[i++], lists[j--]);
                --k;
            }
        }
        return lists[0];
    }
};
```

### Priority Queue: Python

```Python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

import heapq as hq

class priority:
    def __init__(self, p, d):
        self.pr = p
        self.data = d
    
    def __eq__(self, other):
        return self.pr == other.pr
    
    def __lt__(self, other):
        return self.pr < other.pr

class Solution:
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        head = point = ListNode(0)
        q = []
        for l in lists:
            if l:
                hq.heappush(q, priority(l.val, l))
        while q:
            node = hq.heappop(q)
            data = node.data
            point.next = ListNode(data.val)
            data = data.next
            point = point.next
            if data:
                hq.heappush(q, priority(data.val, data))
        return head.next   
```