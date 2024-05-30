# 1st
- 累積和を用いた解法
- `end_sum - start_sum`がsubarrayの和になっていて、kと一致したら`subarray_count`に`start_sum`の個数を追加していく
- `start_sum`subarrayの和を計算するうえで左端にあたる累積和という意味でつけたが変数名が悪いかも。
```py
from collections import defaultdict
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        start_sum_to_count = defaultdict(int)
        start_sum_to_count[0] = 1
        subarray_count = 0
        end_sum = 0
        for i in range(len(nums)):
            end_sum += nums[i]
            start_sum = end_sum - k
            if start_sum in start_sum_to_count:
                subarray_count += start_sum_to_count[start_sum]
            start_sum_to_count[end_sum] += 1
        return subarray_count
```
# 2nd
- https://github.com/ryoooooory/LeetCode/pull/3
  - 1stで`start_sum`や`end_sum`とつけたものは意味をそぎ落とせば累積和になるので`prefix_sum`とつけることにした
- https://github.com/hayashi-ay/leetcode/pull/31/files
  - defaultdict使ってれば`prefix_sum - k`がdictに存在ない時も0が返ってくるので1stのif節は不要
```py
from collections import defaultdict
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        prefix_sum_to_count = defaultdict(int)
        prefix_sum_to_count[0] = 1
        number_of_subarray = 0
        prefix_sum = 0
        for num in nums:
            prefix_sum += num
            number_of_subarray += prefix_sum_to_count[prefix_sum - k]
            prefix_sum_to_count[prefix_sum] += 1
        return number_of_subarray 
``` 
# 3rd
```py
from collections import defaultdict
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        prefix_sum_to_count = defaultdict(int)
        prefix_sum_to_count[0] = 1
        number_of_subarray = 0
        prefix_sum = 0
        for num in nums:
            prefix_sum += num
            number_of_subarray += prefix_sum_to_count[prefix_sum - k]
            prefix_sum_to_count[prefix_sum] += 1
        return number_of_subarray 
```