# 1st
- d_rowは現在のrowと新たに作るnew_rowとの差分(difference)的な意味でつけたがもっと良い変数名がありそう
```py
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        max_row = len(grid[0])
        max_col = len(grid)
        visited = [[False] * max_row for _ in range(max_col)]

        def inside_island(col, row):
            return 0 <= row < max_row and 0 <= col < max_col

        def is_island(col, row):
            return grid[col][row] == "1"

        def visit_island(col, row):
            visited[col][row] = True
            d_row = [0, 0, 1, -1]
            d_col = [1, -1, 0, 0]
            for i in range(4): 
                new_row = row + d_row[i]
                new_col = col + d_col[i]
                if inside_island(new_col, new_row) and is_island(new_col, new_row) and not visited[new_col][new_row]:
                    visit_island(new_col, new_row)

        num_of_islands = 0
        for col in range(max_col):
            for row in range(max_row):
                if is_island(col, row) and not visited[col][row]:
                    num_of_islands += 1
                    visit_island(col, row)
        return num_of_islands
```

# 2nd
DFSでの解法
- https://discord.com/channels/1084280443945353267/1183683738635346001/1194347590125367467
  - stack + loopで書いてもよかった(あまりに島が大きい場合、再帰だとrecursion errorを起こすことがあるかも)
- https://discord.com/channels/1084280443945353267/1200089668901937312/1211329160413323295
  - union findでもできる
```py
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        max_row = len(grid[0])
        max_col = len(grid)
        visited = [[False] * max_row for _ in range(max_col)]

        def inside_island(col, row):
            return 0 <= col < max_col and 0 <= row < max_row

        def is_island(col, row):
            return grid[col][row] == "1"

        def visit_island(col, row):
            visited[col][row] = True
            directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
            for direction in directions:
                new_col = col + direction[0]
                new_row = row + direction[1]
                if inside_island(new_col, new_row) and is_island(new_col, new_row) and not visited[new_col][new_row]:
                    visit_island(new_col, new_row)
        
        number_of_islands = 0
        for col in range(max_col):
            for row in range(max_row):
                if is_island(col, row) and not visited[col][row]:
                    number_of_islands += 1
                    visit_island(col, row)
        return number_of_islands       
```

BFSでも解いた
```py
from collections import deque
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        max_col = len(grid)
        max_row = len(grid[0])
        visited = [[False] * max_row for _ in range(max_col)]

        def inside_island(col, row):
            return 0 <= col < max_col and 0 <= row < max_row
        
        def is_island(col, row):
            return grid[col][row] == "1"
        
        def visit_island(col, row):
            next_visit = deque([(col, row)])
            while next_visit:
                col, row = next_visit.popleft()
                visited[col][row] = True
                directions = [(1, 0), (-1, 0), (0, -1), (0, 1)]
                for direction in directions:
                    new_col = col + direction[0]
                    new_row = row + direction[1]
                    if inside_island(new_col, new_row) and is_island(new_col, new_row) and not visited[new_col][new_row]:
                        next_visit.append((new_col, new_row))
       
        num_of_islands = 0
        for col in range(max_col):
            for row in range(max_row):
                if is_island(col, row) and not visited[col][row]:
                    num_of_islands += 1
                    visit_island(col, row)
        
        return num_of_islands
```

# 3rd
```py
```py
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        max_row = len(grid[0])
        max_col = len(grid)
        visited = [[False] * max_row for _ in range(max_col)]

        def inside_island(col, row):
            return 0 <= col < max_col and 0 <= row < max_row

        def is_island(col, row):
            return grid[col][row] == "1"

        def visit_island(col, row):
            visited[col][row] = True
            directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
            for direction in directions:
                new_col = col + direction[0]
                new_row = row + direction[1]
                if inside_island(new_col, new_row) and is_island(new_col, new_row) and not visited[new_col][new_row]:
                    visit_island(new_col, new_row)
        
        number_of_islands = 0
        for col in range(max_col):
            for row in range(max_row):
                if is_island(col, row) and not visited[col][row]:
                    number_of_islands += 1
                    visit_island(col, row)
        return number_of_islands       
```