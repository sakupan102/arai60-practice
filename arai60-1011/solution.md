# 1st
```py
class Solution:
    def shipWithinDays(self, weights: List[int], days: int) -> int:
        def can_be_shipped(capacity):
            day = 1
            current_weight = 0
            for weight in weights:
                if current_weight + weight > capacity:
                    day += 1
                    current_weight = weight
                    continue
                current_weight += weight
            return day <= days
        
        min_capacity = max(weights)
        max_capacity = sum(weights)
        while min_capacity < max_capacity:
            middle_capacity = (min_capacity + max_capacity) // 2
            if can_be_shipped(middle_capacity):
                max_capacity = middle_capacity
            else:
                min_capacity = middle_capacity + 1
        return min_capacity
```
# 2nd
- https://github.com/hayashi-ay/leetcode/pull/55/files
  - 1stの変数`day`はあまりよくないかも、これを参考に`needed_days`とかにした方がよさそう
```py
class Solution:
    def shipWithinDays(self, weights: List[int], days: int) -> int:
        def can_be_shipped(capacity):
            needed_days = 1
            current_weight = 0
            for weight in weights:
                if current_weight + weight > capacity:
                    needed_days += 1
                    current_weight = weight
                    continue
                current_weight += weight
            return needed_days <= days
        
        min_capacity = max(weights)
        max_capacity = sum(weights)
        while min_capacity < max_capacity:
            middle = (min_capacity + max_capacity) // 2
            if can_be_shipped(middle):
                max_capacity = middle
            else:
                min_capacity = middle + 1
        return min_capacity
```
# 3rd 
```py
class Solution:
    def shipWithinDays(self, weights: List[int], days: int) -> int:
        def can_be_shipped(capacity):
            needed_days = 1
            current_weight = 0
            for weight in weights:
                if current_weight + weight > capacity:
                    needed_days += 1
                    current_weight = weight
                    continue
                current_weight += weight
            return needed_days <= days
        
        min_capacity = max(weights)
        max_capacity = sum(weights)
        while min_capacity < max_capacity:
            middle = (min_capacity + max_capacity) // 2
            if can_be_shipped(middle):
                max_capacity = middle
            else:
                min_capacity = middle + 1
        return min_capacity
```