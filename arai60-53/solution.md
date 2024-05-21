# 1st
- ぱっと思いつくのは`prefix_sum[i] - prefix_sum[j]`の最大値を求めるもの(計算量O(n ** 2))
- `min_prefix_sum[i]`はi番目以前のprefix_sumで最小のものを表している(i番目を含む)
- iを固定した時`prefix_sum[i] - prefix_sum[j]`の最大値は`prefix_sum[i] - min_prefix_sum[i - 1]`で表される
```py
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        def make_prefix_sums(nums):
            prefix_sums = [0] * (len(nums) + 1)
            for i in range(len(nums)):
                prefix_sums[i + 1] = prefix_sums[i] + nums[i]
            return prefix_sums
        prefix_sums = make_prefix_sums(nums)
        def make_min_prefix_sums(prefix_sums):
            min_prefix_sums = [0] * (len(prefix_sums))
            min_prefix_sums[0] = prefix_sums[0]
            for i in range(1, len(prefix_sums)):
                min_prefix_sums[i] = min(min_prefix_sums[i - 1], prefix_sums[i])
            return min_prefix_sums
        min_prefix_sums =  make_min_prefix_sums(prefix_sums)
        max_subarray = prefix_sums[1] - prefix_sums[0]
        for i in range(1, len(prefix_sums)):
            min_prefix_sum = min_prefix_sums[i - 1]
            subarray_sum = prefix_sums[i] - min_prefix_sum
            max_subarray = max(max_subarray, subarray_sum)
        return max_subarray
```
# 2nd
- prefix_sumはmin_prefix_sumとは一つずれているのでしょうがない気がするがprefix_sumとmin_prefix_sumが違うところで更新されているのは少し違和感
```py
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        prefix_sum = 0
        min_prefix_sum = 0
        max_subarray = nums[0]
        for num in nums:
            prefix_sum += num
            max_subarray = max(max_subarray, prefix_sum - min_prefix_sum)
            min_prefix_sum = min(min_prefix_sum, prefix_sum)
        return max_subarray
```

# 3rd
- min_prefix_sumとprefix_sumの更新場所を同じにした
  - ループが始まった瞬間prefix_sumが更新されるのは違和感があるかもしれない
  - ただprefix_sumの更新を後ろにするとループの外で一回max_sumの更新をする必要があるのでどちらも少し違和感が残る
```py
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        max_sum = nums[0]
        prefix_sum = 0
        min_prefix_sum = 0
        for i in range(len(nums)):
            min_prefix_sum = min(min_prefix_sum, prefix_sum)
            prefix_sum = prefix_sum + nums[i]
            max_sum = max(max_sum, prefix_sum - min_prefix_sum)
        return max_sum
```
