# 877. Stone Game
https://leetcode.com/problems/stone-game/

# Description
Alex and Lee play a game with piles of stones.  There are an even number of piles arranged in a row, and each pile has a positive integer number of stones piles[i].

The objective of the game is to end with the most stones.  The total number of stones is odd, so there are no ties.

Alex and Lee take turns, with Alex starting first.  Each turn, a player takes the entire pile of stones from either the beginning or the end of the row.  This continues until there are no more piles left, at which point the person with the most stones wins.

Assuming Alex and Lee play optimally, return True if and only if Alex wins the game.

 
# Example

**Input**: [5,3,4,5]

**Output**: true

**Explanation**: 
Alex starts first, and can only take the first 5 or the last 5.
Say he takes the first 5, so that the row becomes [3, 4, 5].
If Lee takes 3, then the board is [4, 5], and Alex takes 5 to win with 10 points.
If Lee takes the last 5, then the board is [3, 4], and Alex takes 4 to win with 9 points.
This demonstrated that taking the first 5 was a winning move for Alex, so we return true.
 
# Limitation
- 2 <= `piles.length` <= 500
- `piles.length` is even.
- 1 <= `piles[i]` <= 500
- `sum(piles)` is odd.

# Solution 1
## Explanation
此題目的是要回答 Alex 是否能贏過 Lee，而題目說了共有偶數堆石頭，而石頭總和數目為奇數。因此我們可以得知下列情形必有其一成立：
- `sum(piles[even])` > `sum(piles[odd])`
- `sum(piles[even])` < `sum(piles[odd])`

關鍵在於，Alex 是先選擇的人，他可以決定自己要拿到所有位於偶數位置的石頭堆，或是所有位於奇數位置的石頭堆。  
例如 Alex 發現位於偶數位置石頭堆總和較大，他便先選擇 `piles[0]`，而 Lee 只能選擇 `piles[1]` 或 `piles[n-1]`，皆為奇數位置的石頭堆。不論 Lee 如何選擇，Alex 下一次選擇都能再選擇偶數位置的石頭堆，於是直到最後，Alex 能選到所有位於偶數位置的石頭堆。反正亦然，Alex 也能選擇所有位於奇數位置的石頭堆。  
所以此遊戲便是先選擇的人必定會獲勝。  

## Source Code
```python
class Solution:
    def stoneGame(self, piles: 'List[int]') -> 'bool':
        return True
```

## Analysis
- Time: `O(1)`
- Space: `O(1)`

# Solution 2
## Explanation
定義一個二維陣列，其中 `dp[i][j]` 表示從 `piles[i]` 至 `piles[j]` 中，Alex 與 Lee 的石頭差異數量最大化。  
例如 Alex 先選擇，他可以選 `piles[i]` 或是 `piles[j]`：  
1. 若 Alex 選擇 `piles[i]`，則其結果是 `piles[i] - dp[i + 1][j]`
2. 若 Alex 選擇 `piles[j]`，則其結果是 `piles[j] - dp[i][j - 1]`

若輸入為 `[5,3,4,5]`，則 `dp[1][3]` 表示 `piles[1]` 至 `piles[3]` 中，Alex 所能拿到的石頭數量，減掉 Lee 所能拿到的石頭數量最大化，其結果為 4。因為 Alex 先選，而他能選到 `piles[3]` 及 `piles[1]`，而 Lee 能選到 `piles[2]`，其差異為 4。  

所以能得出下列公式：  
`dp[i][j] = max(piles[i] - dp[i + 1][j], piles[j] - dp[i][j - 1])`


## Source Code
```python
class Solution:
    def stoneGame(self, piles: 'List[int]') -> 'bool':
        n = len(piles)
        dp = [[0] * n for i in range(n)]
        for i in range(n):
            dp[i][i] = piles[i]
        for d in range(1, n):
            for i in range(n - d):
                dp[i][i + d] = max(piles[i] - dp[i + 1][i + d], piles[i + d] - dp[i][i + d -1])
        return dp[0][-1] > 0
```

## Analysis
- Time: `O(n^2)`
- Space: `O(n^2)`

# Remark
- https://www.youtube.com/watch?v=WxpIHvsu1RI