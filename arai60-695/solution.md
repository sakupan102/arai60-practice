# 1st
BFSでの解法
-  `if is_island(row, col) and not visited[row][col]:`を満たすときだけ`count_size_of_island`を呼び出しているが、これを満たさないときは0を返して常に呼び出すようにしてもいいかも
```py
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        num_rows = len(grid)
        num_cols = len(grid[0])
        visited = [[False] * num_cols for _ in range(num_rows)]

        def inside_grid(row, col):
            return 0 <= row < num_rows and 0 <= col < num_cols
        
        def is_island(row, col):
            return grid[row][col] == 1
        
        def count_size_of_island(row, col):
            visited[row][col] = True
            directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
            size_of_island = 1
            for direction in directions:
                new_row = row + direction[0]
                new_col = col + direction[1]
                if inside_grid(new_row, new_col) and is_island(new_row, new_col) and not visited[new_row][new_col]:
                    size_of_island += count_size_of_island(new_row, new_col)
            return size_of_island
        
        max_area_of_island = 0
        for row in range(num_rows):
            for col in range(num_cols):
                if is_island(row, col) and not visited[row][col]:
                    size_of_island = count_size_of_island(row, col)
                    max_area_of_island = max(max_area_of_island, size_of_island)
        return max_area_of_island
```

# 2nd
- https://github.com/hayashi-ay/leetcode/pull/34/files
  - gridを書き換えることによってvisitedを使わずに済んでいる
  - 副作用があるのでメモリに不安のない場合はvisitedを用いた方がいいかも　
DFSで解いた
```py
from collections import deque
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        num_rows = len(grid)
        num_cols = len(grid[0])
        visited = [[False] * num_cols for _ in range(num_rows)]

        def inside_grid(row, col):
            return 0 <= row < num_rows and 0 <= col < num_cols
        
        def is_island(row, col):
            return grid[row][col] == 1
        
        def count_size_of_island(row, col):
            visited[row][col] = True
            next_visit = deque([(row, col)])
            size_of_island = 0
            while next_visit:
                row, col = next_visit.popleft()
                size_of_island += 1
                directions = [(1, 0), (-1, 0), (0, -1), (0, 1)]
                for direction in directions:
                    new_row = row + direction[0]
                    new_col = col + direction[1]
                    if inside_grid(new_row, new_col) and is_island(new_row, new_col) and not visited[new_row][new_col]:
                        visited[new_row][new_col] = True
                        next_visit.append((new_row, new_col))
            return size_of_island

        
        max_area_of_island = 0
        for row in range(num_rows):
            for col in range(num_cols):
                if is_island(row, col) and not visited[row][col]:
                    size_of_island = count_size_of_island(row, col)
                    max_area_of_island = max(max_area_of_island, size_of_island)
        return max_area_of_island
```

# 3rd
```py
from collections import deque
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        num_rows = len(grid)
        num_cols = len(grid[0])
        visited = [[False] * num_cols for _ in range(num_rows)]

        def inside_grid(row, col):
            return 0 <= row < num_rows and 0 <= col < num_cols
        
        def is_island(row, col):
           return grid[row][col] == 1
        

        def count_size_of_island(row, col):
            next_visit = deque([(row, col)])
            visited[row][col] = True
            size_of_island = 1
            while next_visit:
                row, col = next_visit.popleft()
                directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
                for direction in directions:
                    new_row = direction[0] + row
                    new_col = direction[1] + col
                    if inside_grid(new_row, new_col) and is_island(new_row, new_col) and not visited[new_row][new_col]:
                        size_of_island += 1
                        visited[new_row][new_col] = True
                        next_visit.append((new_row, new_col))
            return size_of_island
        
        max_size_of_island = 0
        for row in range(num_rows):
            for col in range(num_cols):
                if is_island(row, col) and not visited[row][col]:
                    size_of_island = count_size_of_island(row, col)
                    max_size_of_island = max(max_size_of_island, size_of_island)
        return max_size_of_island
```
