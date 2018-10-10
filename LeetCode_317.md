# 317. Shortest Distance from All Buildings

Problem link: [317. Shortest Distance from All Buildings](https://leetcode.com/problems/shortest-distance-from-all-buildings/description/)

* Level: [Hard](https://leetcode.com/problemset/all/?difficulty=Hard)
* Appears in: [Google Interview](https://leetcode.com/explore/interview/card/google/)

## Hints

### Intuition

It is straightforward to think about traversing all the 0 nodes and using BFS to find shortest paths. However, it's obvious that this method is very time wasted, because you will traverse each building more than once. So, if you think inversely that start from each building and find its shortest path to each 0 node, and then sum the distance up at each 0 node then you get the shortest distances. Finally, you just have to pick the smallest one from the grid.

## Implementation

### Python (beats 70%)
```Python
class Solution:
    def shortestDistance(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        size_r = len(grid)
        size_c = len(grid[0])
        dist = [[0 for i in range(size_c)] for j in range(size_r)]
        bfs_queue =  collections.deque([])
        num_building = 0
        
        for i in range(size_r):
            for j in range(size_c):
                if grid[i][j] == 1:
                    bfs_queue.append((i + 1, j, 1))
                    bfs_queue.append((i, j + 1, 1))
                    bfs_queue.append((i - 1, j, 1))
                    bfs_queue.append((i, j - 1, 1))
                    while len(bfs_queue) > 0:
                        x, y, dis = bfs_queue.popleft()
                        if (x >= 0 and x < size_r) and (y >= 0 and y < size_c) and grid[x][y] == -num_building:
                            dist[x][y] += dis
                            grid[x][y] -= 1
                            bfs_queue.append((x + 1, y, dis + 1))
                            bfs_queue.append((x, y + 1, dis + 1))
                            bfs_queue.append((x - 1, y, dis + 1))
                            bfs_queue.append((x, y - 1, dis + 1))
                    num_building += 1
        
        min_dis = -1
        for i in range(size_r):
            for j in range(size_c):
                if grid[i][j] + num_building == 0:
                    if min_dis == -1 or dist[i][j] < min_dis:
                        min_dis = dist[i][j]
        return min_dis
```