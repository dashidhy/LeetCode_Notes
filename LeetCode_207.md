# 207. Course Schedule

Problem link: [207. Course Schedule](https://leetcode.com/problems/course-schedule/description/)

* Level: [Medium](https://leetcode.com/problemset/all/?difficulty=Medium)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

This problem is about how to detect a circle in directed graphs. Both DFS and BFS (a modified version) can solve this problem. DFS is straightforward: if you find a new node is already in the current route, you find a circle. To use BFS, you should visit a new node if and only if all of it's parents have been visited, in this way a node on a circle will never be visited because it is itself's decendant, so after you finished the BFS process, if some of the nodes are not visited, you find a circle. To compare the time complexity, the larger the circles are, the faster BFS is, since you won't visit the nodes on the circles, while DFS is slower because in the worst case you have to visit all the nodes in the graph and it has nothing to do with the size of the circle.

## Implementation

### DFS: Python (beats 77.09%)
```Python
class Solution:
    def canFinish(self, num_V, E):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        
        graph = {} # parent: [child[], int]
        dfs = [] # stack for DFS
        
        # build the graph
        for edge in E:
            if edge[0] not in graph:
                graph[edge[0]] = [[], 0]
            if edge[1] not in graph:
                graph[edge[1]] = [[], 0]
            graph[edge[1]][0].append(edge[0])
        
        for v in graph:
            if graph[v][1] == 0: # never visited
                p = v
                graph[p][1] = 1 # status 0 for never visited, 1 for in stack, 2 for visited
                dfs.append(p)
                while dfs:
                    if graph[dfs[-1]][0]:
                        p = graph[dfs[-1]][0].pop()
                        if graph[p][1] == 1: # find a circle
                            return False
                        elif graph[p][1] == 0:
                            graph[p][1] = 1
                            dfs.append(p)
                    else:
                        p = dfs.pop()
                        graph[p][1] = 2
        
        return True
```

### BFS: Python (beats 100%)

```Python
from collections import defaultdict
class Solution:
    def canFinish(self, numCourses, prerequisites):
        preNumList = [0]*numCourses
        preDict = defaultdict(list)
        freeCourses = []
        for pair in prerequisites:
            preNumList[pair[0]]+=1
            preDict[pair[1]].append(pair[0])
            
        for i in range(len(preNumList)):
            if preNumList[i] == 0:
                freeCourses.append(i)
        for fc in freeCourses:
            for i in preDict[fc]:
                preNumList[i] -=1
                if preNumList[i] == 0:
                    freeCourses.append(i)
            
        return len(freeCourses) == numCourses
```