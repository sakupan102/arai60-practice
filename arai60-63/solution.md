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