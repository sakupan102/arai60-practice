# 1st
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
