# 1st
- 縦に`m -1`回、横に`n - 1`回進むのでその並び替えに関する問題
- `(m + n - 2) C (n -1)`を解けばよい
- `unique_path_helper`の`row`,`col`は実際のrow, colに対応していないので若干違和感がある。
  - `unique_path_helper`を`combination`とかに変えてもいいかも
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        cache = [[-1] * (n) for _ in range(m + n - 1)]
        def unique_paths_helper(row, col):
            if row == 0 or col == 0 or row == col:
                return 1
            if cache[row][col] != -1:
                return cache[row][col]
            cache[row][col] = unique_paths_helper(row - 1, col) + unique_paths_helper(row - 1, col - 1)
            return cache[row][col]
        return unique_paths_helper(m + n - 2, n - 1)
```
# 2nd 
## メモ化再帰
- https://github.com/hayashi-ay/leetcode/pull/39/files
  - math.combも使える
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        combinations_cache = [[-1] * (n) for _ in range(n + m - 1)]
        def combinations(x, y): 
            if x == 0 or y == 0 or x == y:
                return 1
            if combinations_cache[x][y] != -1:
                return combinations_cache[x][y]
            result = combinations(x - 1, y) + combinations(x - 1, y - 1)
            combinations_cache[x][y] = result
            return result
        return combinations(n + m - 2, n - 1)
```

## 2DPの解法
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        ways = [[1] * n for _ in range(m)]
        for row in range(m):
            for col in range(n):
                if row == 0 or col == 0:
                    continue
                ways[row][col] = ways[row - 1][col] + ways[row][col - 1]
        return ways[-1][-1]
```

## 1DP
- `ways`とか`new_ways`とかの変数名が分かりにくいwaysで着目しているrowの値は一緒なので`same_row_num_ways`とかでもいいかも
- https://github.com/hayashi-ay/leetcode/pull/39/files
  - `for row in range(1, m)`としていて今着目しているrowの値を処理の対応が分かりやすい
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        ways = [1] * n
        for _ in range(m - 1):
            new_ways = [1] * n
            for col in range(1, n):
                new_ways[col] = ways[col] + new_ways[col - 1]
            ways = new_ways
        return ways[-1]
```
# 3rd
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        same_row_num_ways = [1] * n
        for row in range(1, m):
            for col in range(1, n):
                same_row_num_ways[col] = same_row_num_ways[col - 1] + same_row_num_ways[col]
        return same_row_num_ways[-1]
```

# 4th
cacheを用いた再帰
```py
from functools import cache
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        @cache
        def combinations(n, k):
            if n == 0 or k == 0 or n == k:
                return 1
            return combinations(n - 1, k) + combinations(n - 1, k - 1)
        
        return combinations(m + n - 2, m - 1)
```