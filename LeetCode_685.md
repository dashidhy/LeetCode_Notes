# 685. Redundant Connection II

Problem link: [685. Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

Basic union-find algorithm while the corner cases are difficult to handle. An edge can cause two kinds of conflicts, the first is parent conflict that a child has two different parents, the second is circle. An important fact is that the two kinds of conflict could happen simultaneously caused by one edge.

## Implementation

### Python (beats 85.52%)
```Python
class Solution:
    def findRedundantDirectedConnection(self, edges):
        """
        :type edges: List[List[int]]
        :rtype: List[int]
        """
        
        root = {}
        parent = {}
        conflict_edges = []
        circle_edges = []
        conflict = False
        circle = False
        
        for l in edges:
            
            if root.get(l[1], l[1]) != l[1]: # parent conflict
                conflict = True
                if circle:
                    return l if l in circle_edges else [parent[l[1]], l[1]]
                conflict_edges.append(l)
                conflict_edges.append([parent[l[1]], l[1]])
                continue # do not archive l
            
            if l[0] in root:
                c = l[0]
                while root[c] != c:
                    if root[c] == l[1]: # circle
                        circle = True
                        circle_edges.append(l)
                        c = l[0]
                        while c in parent:
                            circle_edges.append([parent[c], c])
                            c = parent[c]
                        if conflict:
                            return conflict_edges[0] if conflict_edges[0] in circle_edges else conflict_edges[1]
                        break
                    c = root[c]
                                              
            parent[l[1]] = l[0] # add edge for fast lookup
            if l[0] not in root: # union-find
                root[l[0]] = l[0]
            root[l[1]] = root[l[0]]
            
        return conflict_edges[0] if conflict_edges else circle_edges[0]
```