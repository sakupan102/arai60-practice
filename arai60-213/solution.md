# 1st
- 右端を含む場合と含まない場合を分けて考えた
```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]
            
        def rob_house(nums):
            if len(nums) <= 2:
                return max(nums, default = 0)
            max_sum = [0] * len(nums)
            max_sum[0] = nums[0]
            max_sum[1] = max(nums[0], nums[1])
            for i in range(2, len(nums)):
                max_sum[i] = max(max_sum[i - 1], max_sum[i - 2] + nums[i])
            return max_sum[-1]
        
        return max(rob_house(nums[0: len(nums) - 1]), rob_house(nums[1: len(nums)]))
```

# 2nd
- https://github.com/hayashi-ay/leetcode/pull/50/files
  - `nums[1: len(nums)]`よりも`nums[1:]`の方が簡潔で分かりやすかった
  - 一直線の家の並びを意識しているので`rob_house_in_line`に変更した。
```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]
        
        def rob_house_in_line(nums):
            if len(nums) <= 2:
                return max(nums)
            max_amount = [0] * len(nums)
            max_amount[0] = nums[0]
            max_amount[1] = max(nums[0], nums[1])
            for i in range(2, len(nums)):
                max_amount[i] = max(max_amount[i - 1], max_amount[i - 2] + nums[i])
            return max_amount[-1]
        
        return max(rob_house_in_line(nums[1:]), rob_house_in_line(nums[:-1]))
```

# 3rd
```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]
        
        def rob_house_in_line(nums):
            if len(nums) <= 2:
                return max(nums)
            max_amount = [0] * len(nums)
            max_amount[0] = nums[0]
            max_amount[1] = max(nums[0], nums[1])
            for i in range(2, len(nums)):
                max_amount[i] = max(max_amount[i - 1], max_amount[i - 2] + nums[i])
            return max_amount[-1]
        
        return max(rob_house_in_line(nums[1:]), rob_house_in_line(nums[:-1]))
```