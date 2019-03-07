# 797. All Paths From Source to Target
https://leetcode.com/problems/all-paths-from-source-to-target/

# Description
Given a directed, acyclic graph of `N` nodes.  Find all possible paths from node `0` to node `N-1`, and return them in any order.  
The graph is given as follows:  the nodes are 0, 1, ..., graph.length - 1.  `graph[i]` is a list of all nodes `j` for which the edge `(i, j)` exists.

# Example
**Input**: [[1,2], [3], [3], []] 

**Output**: [[0,1,3],[0,2,3]] 

**Explanation**:  
The graph looks like this:
```
0--->1
|    |
v    v
2--->3
```
There are two paths: `0 -> 1 -> 3` and `0 -> 2 -> 3`.

# Limitation
- The number of nodes in the graph will be in the range `[2, 15]`.
- You can print different paths in any order, but you should keep the order of nodes inside one path.

# Solution 1
## Explanation
此題可利用 DFS 來解，我們只需從第一個 node 沿著 edge 走，並同時紀錄 path，若能走到最後一個 node 便將 path 加到答案裡。其中若有多條 edge，便根據先前的 path 分岔出去。  
由於有特別說明是無環圖，所以不需考慮環的情形，事實上若是有環，則要列出所有 path 是不可能的，其組合為無限多種，因為只要多繞一圈環，便能多一條 path 出來。

## Source Code
```python
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
        def dfs(cur, path):
            if cur == len(graph)-1:
                res.append(path)
            else:
                for i in graph[cur]:
                    dfs(i, path + [i])
        res = []
        dfs(0, [0])
        return res
```

## Analysis
- Time: `O(n!)`
- Space: `O(n!)`
