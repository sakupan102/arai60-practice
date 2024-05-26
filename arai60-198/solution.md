# 1st
- `max_sum_money[i]`はi番目以前の金とi番目の金を盗んだ時の最大金額を表している
- time complexity: O(N ** 2)
- space O(N)
```py
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        max_sum_money = [0] * len(nums)
        max_sum_money[0] = nums[0]
        for i in range(1, len(nums)):
            max_sum_before_i = 0
            for j in range(0, i - 1):
                max_sum_before_i = max(max_sum_before_i, max_sum_money[j])
            max_sum_money[i] = max_sum_before_i + nums[i]
        return max(max_sum_money)
```

# 2nd
- https://github.com/shining-ai/leetcode/pull/35/files
  - i番目を含む左側の家の金を盗んだ時の最大金額にすればtime complexity: O(N)で解ける
