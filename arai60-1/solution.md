# 1st
- `pair_val_to_index`はペアとなる値と自分のインデックスの辞書という意味だが、伝わらないかも
- 自分の値と自分のインデックスを持たせた方が良い
```py
from collections import defaultdict
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_to_index = defaultdict(int)
        for i in range(len(nums)):
            if nums[i] in num_to_index:
                the_other_index = num_to_index[nums[i]]
                return [the_other_index, i]
            num_to_index[target - nums[i]] = i
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
            the_other = target - nums[i]
            if the_other in num_to_index:
                the_other_index = num_to_index[the_other]
                return [the_other_index, i]
            num_to_index[nums[i]] = i
        return None
```
# 3rd
```py
from collections import defaultdict
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_to_index = defaultdict(int)
        for index, num in enumerate(nums):
            the_other = target - num
            if the_other in num_to_index:
                the_other_index = num_to_index[the_other]
                return [the_other_index, index]
            num_to_index[num] = index
        return []
```
