# 1st 
```py
import math
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        inf = math.inf
        num_fewest_coins = [inf] * (amount + 1)
        num_fewest_coins[0] = 0
        for current_amount in range(1, len(num_fewest_coins)):
            for coin in coins:
                prev_amount = current_amount - coin
                if prev_amount >= 0 and num_fewest_coins[prev_amount] != inf:
                    num_fewest_coins[current_amount] = min(num_fewest_coins[current_amount], num_fewest_coins[prev_amount] + 1)
        if num_fewest_coins[-1] == inf:
            return -1
        return num_fewest_coins[-1]
```
# 2nd
- https://github.com/hayashi-ay/leetcode/pull/68/files
  - `prev_amount < 0`のときearly returnする方が良いかも
```py
import math
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        inf = math.inf
        num_fewest_coins = [inf] * (amount + 1)
        num_fewest_coins[0] = 0
        for sum_coin in range(1, amount + 1):
            for coin in coins:
                prev_sum = sum_coin - coin
                if prev_sum < 0:
                    continue
                num_fewest_coins[sum_coin] = min(num_fewest_coins[sum_coin], num_fewest_coins[prev_sum] + 1)
        if num_fewest_coins[-1] == inf:
            return -1
        return num_fewest_coins[-1]
```
# 3rd
```py
import math
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        inf = math.inf
        num_fewest_coins = [inf] * (amount + 1)
        num_fewest_coins[0] = 0
        for sum_coin in range(1, amount + 1):
            for coin in coins:
                prev_sum = sum_coin - coin
                if prev_sum < 0:
                    continue
                num_fewest_coins[sum_coin] = min(num_fewest_coins[sum_coin], num_fewest_coins[prev_sum] + 1)
        if num_fewest_coins[-1] == inf:
            return -1
        return num_fewest_coins[-1]
```