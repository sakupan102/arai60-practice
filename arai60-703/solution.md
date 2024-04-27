# 1st
- ヒープに入れる操作はinitでもaddでも同じなので処理をaddのほうにまとめた
```python
import heapq
class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        self.top_k_nums = []
        self.limit = k
        for num in nums:
            self.add(num)

    def add(self, number):
        heapq.heappush(self.top_k_nums, number)
        if len(self.top_k_nums) > self.limit:
            heapq.heappop(self.top_k_nums)
        return self.top_k_nums[0]
```
# 2nd
- 1stとほぼ同じ
- https://discord.com/channels/1084280443945353267/1195700948786491403/1198906453197606932
    - 処理を共通化してない以外はじぶんとほぼ同じ
- 共通の処理は第三の関数を定義してそこで処理してもいいかも
```python
import heapq
class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        self.top_nums = []
        self.limit = k
        for num in nums:
            self.add(num)

    def add(self, num):
        heapq.heappush(self.top_nums, num)
        if len(self.top_nums) > self.limit:
            heapq.heappop(self.top_nums)
        return self.top_nums[0]
```
# 3rd
```python
import heapq
class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        self.top_k_nums = []
        self.limit = k
        for num in nums:
            self.add(num)
            
    def add(self, num):
        heapq.heappush(self.top_k_nums, num)
        if len(self.top_k_nums) > self.limit:
            heapq.heappop(self.top_k_nums)
        return self.top_k_nums[0]
```
# TODO
- heapの実装