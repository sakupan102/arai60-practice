# 1st
- 上昇しているときに売り買いをすればよいので上がり始めに買って下がり始めに売ればよい
```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        max_profit = 0
        for i in range(1, len(prices)):
            if prices[i] <= prices[i - 1]:
                continue
            max_profit += prices[i] - prices[i - 1]
        return max_profit
```

# 2nd
- https://github.com/hayashi-ay/leetcode/pull/56/files
  - 株を持っているときと持っていないときの最大利益をループで更新させる方法もある
  - 底と天井を見つけて売り買いする方法もある
```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        max_profit = 0
        for i in range(1, len(prices)):
            if prices[i] <= prices[i - 1]:
                continue
            max_profit += prices[i] - prices[i - 1]
        return max_profit
```

# 3rd
```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        max_profit = 0
        for i in range(1, len(prices)):
            if prices[i] <= prices[i - 1]:
                continue
            max_profit += prices[i] - prices[i - 1]
        return max_profit
```
