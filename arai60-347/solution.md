# 1st
```python
from collections import defaultdict
import heapq
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        num_frequency = defaultdict(int)
        top_frequent_nums = []
        top_k_nums = []
        for num in nums:
            num_frequency[num] += 1
        for num in num_frequency:
            heapq.heappush(top_frequent_nums, (-num_frequency[num], num))
        for i in range(k):
            _, num = heapq.heappop(top_frequent_nums)
            top_k_nums.append(num)
        return top_k_nums
```
# 2nd 
- https://github.com/YukiMichishita/LeetCode/pull/3/files#diff-1897b7a4643771fb323fe5359b1c63a3cf56fec3f14f3271974b6c5cc9231340
    - `for num, frequency in nums_to_count.items():`ってできるの知らなかった
- https://github.com/YukiMichishita/LeetCode/pull/3/files#diff-36345f1a68047c1e6115ff93e039240db986e0f001b2b7aa192613739057a8e7
  - quick selectでも解ける
```py
from collections import defaultdict
import heapq
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        num_to_count = defaultdict(int)
        num_frequency_heap = []
        top_k_nums = []
        for num in nums:
            num_to_count[num] += 1
        for num , count in num_to_count.items():
            heapq.heappush(num_frequency_heap, (-count, num))
        for _ in range(k):
            _, num = heapq.heappop(num_frequency_heap)
            top_k_nums.append(num)
        return top_k_nums
```

# 3rd
```py
from collections import defaultdict
import heapq
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        num_to_count = defaultdict(int)
        num_frequency_heap = []
        top_k_frequent_nums = []
        for num in nums:
            num_to_count[num] += 1
        for num, count in num_to_count.items():
            heapq.heappush(num_frequency_heap, (-count, num))
        for _ in range(k):
            _, num = heapq.heappop(num_frequency_heap)
            top_k_frequent_nums.append(num)
        return top_k_frequent_nums
```

# defaultdictの実装
- クラスのメンバにdictを持たせて実装
- new_dict[3]はnew_dict.__getitem__(3)のsyntax sugar
```py
class my_default_dict:
  def __init__(self, function):
    self.function = function
    self.dict = dict()

  def __setitem__(self, key, value):
    self.dict[key] = value

  def __getitem__(self, key):
    if key in self.dict:
      return self.dict[key]
    else:
      self.dict[key] = self.function()
      return self.dict[key]

new_dict = my_default_dict(int)
new_dict[3] = 9
print(new_dict[3]) # 9
print(new_dicts[7]) # 0
```