# 1st
- indexより後ろの最小価格を見て`max_profit`を更新していく解法
```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = prices[0]
        max_profit = 0
        for i in range(1, len(prices)):
            max_profit = max(max_profit, prices[i] - min_price)
            min_price = min(min_price, prices[i])
        return max_profit
```
# 2nd
- 特に変更したところなし
- しいて言うなら`for price in prices[1:]`とかにしてもよかったかも
```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = prices[0]
        max_profit = 0
        for i in range(1, len(prices)):
            max_profit = max(max_profit, prices[i] - min_price)
            min_price = min(prices[i], min_price)
        return max_profit
```

# 3rd
```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = prices[0]
        max_profit = 0
        for i in range(1, len(prices)):
            max_profit = max(max_profit, prices[i] - min_price)
            min_price = min(prices[i], min_price)
        return max_profit
```
