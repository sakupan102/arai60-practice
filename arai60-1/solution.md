# 1st
- `pair_val_to_index`はペアとなる値と自分のインデックスの辞書という意味だが、伝わらないかも
- 自分の値と自分のインデックスを持たせた方が良い
```py
from collections import defaultdict
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        pair_val_to_index = defaultdict(int)
        for i in range(len(nums)):
            if nums[i] in pair_val_to_index:
                pair_index = pair_val_to_index[nums[i]]
                return [pair_index, i]
            pair_val_to_index[target - nums[i]] = i
```
# 2nd
- https://discord.com/channels/1084280443945353267/1226508154833993788/1227088321537376296
  - 今回は大丈夫だが、ペアが見つからなかったときの処理も考えた方がいい
  - 空で返す、エラーを投げる等が考えられる、プログラムの終了などが考えられる。
```py
from collections import defaultdict
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_to_index = defaultdict(int)
        for i in range(len(nums)):
            pair_num = target - nums[i]
            if pair_num in num_to_index:
                pair_index = num_to_index[pair_num]
                return [pair_index, i]
            num_to_index[nums[i]] = i
        return None
```
# 3rd
```py
from collections import defaultdict
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_to_index = defaultdict(int)
        for i in range(len(nums)):
            pair_num = target - nums[i]
            if pair_num in num_to_index:
                pair_index = num_to_index[pair_num]
                return [pair_index, i]
            num_to_index[nums[i]] = i
        return []
```
