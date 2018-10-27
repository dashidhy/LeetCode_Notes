# 924. Minimize Malware Spread

Problem link: [924. Minimize Malware Spread](https://leetcode.com/contest/weekly-contest-106/problems/minimize-malware-spread/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Weekly Contest 106](https://leetcode.com/contest/weekly-contest-106)

## Hints

### Intuition

If a connected component of the graph contains one malware node, removing the node will save the whole component. On the other hand, if it contains 2 or more malware nodes, the component won't be saved. So what we want to do is to find the largest connected component which contains only one malware node, or if all the components contains more than one malware node, return the smallest index of malware nodes.

One trick we can do to reduce the complexity of our algorithm is we break the search process when we find two malware node in a component. This trick can change the efficiency of the algorithm from time limit exceeded to beats 99%.

## Implementation

### Python (beats 99%)
```Python
class Solution:
    def minMalwareSpread(self, graph, initial):
        """
        :type graph: List[List[int]]
        :type initial: List[int]
        :rtype: int
        """
        N = len(graph)
        dic_size = collections.defaultdict(int)
        init = set(initial)
        for n in initial:
            if graph[n][n] == 1:
                q = collections.deque([])
                q.append(n)
                stop = True
                while q and stop:
                    node = q.popleft()
                    graph[node][node] = 0
                    dic_size[n] += 1
                    for i in range(N):
                        if graph[i][node] == 1:
                            if i in init and i is not n:
                                graph[i][i] = 0
                                del dic_size[n]
                                stop = False
                                break
                            elif graph[i][i] == 1:
                                q.append(i)
        if dic_size:
            max_size = 0
            for key in dic_size:
                if dic_size[key] > max_size or (dic_size[key] == max_size and idx > key):
                    max_size = dic_size[key]
                    idx = key
            return idx
        else:
            return min(initial)
```