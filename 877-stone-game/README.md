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
DP

## Source Code

## Analysis