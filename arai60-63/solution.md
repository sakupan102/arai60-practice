# 1st
```py
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        num_ways = [[0] * len(obstacleGrid[0]) for _ in range(len(obstacleGrid))]
        for row in range(len(obstacleGrid)):
            for col in range(len(obstacleGrid[0])):
                if obstacleGrid[row][col] == 1:
                    continue
                if row == 0 and col == 0:
                    num_ways[row][col] = 1
                if row > 0:
                    num_ways[row][col] += num_ways[row -1][col]
                if col > 0:
                    num_ways[row][col] += num_ways[row][col - 1]
        return num_ways[-1][-1]
```

# 2nd
- https://github.com/shining-ai/leetcode/pull/34/files
  - `num_rows`, `num_cols`を定義してもよかった。
  - コードの行数が多くなる場合`OBSTACLE`と`SPACE`も必要か
```py
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):   
        num_ways = [[0] * len(obstacleGrid[0]) for _ in range(len(obstacleGrid))]
        num_ways[0][0] = 1
        for row in range(len(obstacleGrid)):
            for col in range(len(obstacleGrid[0])):
                if obstacleGrid[row][col] == 1:
                    num_ways[row][col] = 0
                    continue
                if row > 0:
                    num_ways[row][col] += num_ways[row - 1][col]
                if col > 0:
                    num_ways[row][col] += num_ways[row][col - 1]
        return num_ways[-1][-1]
```

# 3rd
```py
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):   
        num_ways = [0] * len(obstacleGrid[0])
        num_ways[0] = 1
        for row in range(len(obstacleGrid)):
            for col in range(len(obstacleGrid[0])):
                if obstacleGrid[row][col] == 1:
                    num_ways[col] = 0
                    continue
                if col > 0:
                    num_ways[col] += num_ways[col - 1]
        return num_ways[-1]
```
