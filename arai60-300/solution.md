# 1st
- 変数名に入れるべき内容が多いので困った
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        len_longest_increasing_subsequence = [0] * len(nums)
        len_longest_increasing_subsequence[0] = 1
        for i in range(1, len(nums)):
            max_length = 1
            for j in range(0, i):
                if nums[i] > nums[j]:
                    max_length = max(max_length, len_longest_increasing_subsequence[j] + 1)
            len_longest_increasing_subsequence[i] = max_length
        return max(len_longest_increasing_subsequence)
```

# 2nd 
- https://github.com/hayashi-ay/leetcode/pull/27/files
  - `len_LIS[i]`は「iで終わるLISの長さという意味」なので`max_lis_lengths_ending_with_itself`という名前も考えられる
  - コメントで書く方法を採用した
- `get_len_LIS`も微妙なところ
  - 「`target_index`より左で`nums[target_index]`よりも小さい値で終わる最大の部分列の長さ」を取得する関数だが全ての要素を変数名に入れるのは難しい
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        def get_len_LIS(target_index): # get LIS length before target index and end with smaller value
            max_length = 0
            for i in range(target_index):
                if nums[i] < nums[target_index]:
                    max_length = max(max_length, len_LIS[i])
            return max_length
        len_LIS = [0] * len(nums) #len_LIS[i]: length of LIS end with i
        max_length = 0
        for i in range(len(nums)):
            len_LIS[i] = get_len_LIS(i) + 1
            max_length = max(max_length, len_LIS[i])
        return max_length
```

# 3rd
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        LIS_length = [0] * len(nums) #LIS_length[i]: length of LIS ending with i
        
        def get_LIS_length_before_target_index(target_index): #return LIS length before target and end wigh smaller value
            max_length = 0
            for i in range(target_index):
                if nums[i] < nums[target_index]:
                    max_length = max(max_length, LIS_length[i])
            return max_length
        
        for i in range(len(nums)):
            LIS_length[i] = get_LIS_length_before_target_index(i) + 1
        return max(LIS_length)
```

# 二分探査を用いたO(N log(N))の解法
## 1st
- `if tail_nums[middle] == num`のときmiddleをleftとりrightに代入させてループを脱出させるのはやや不自然か
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        inf = math.inf
        tail_nums = [inf] * len(nums)
        for num in nums:
            left = 0
            right = len(nums) - 1
            while left < right:
                middle = (left + right) // 2
                if tail_nums[middle] == num:
                    left, right = middle, middle
                    continue
                if num < tail_nums[middle]:
                    right = middle
                    continue
                left = middle + 1
            tail_nums[right] = num

        len_subsequence = 0
        while len_subsequence < len(tail_nums) and tail_nums[len_subsequence] < inf:
            len_subsequence += 1
        return len_subsequence
```

# 2nd
- while else文を用いて条件分岐後の処理を分けた。
> 頭から舐めていって k 番目まで見たときに、
「nums[k] までを使って、すべての長さ1のシーケンスを考えたときに、そのシーケンスの一番お尻の最小値」
「nums[k] までを使って、すべての長さ2のシーケンスを考えたときに、そのシーケンスの一番お尻の最小値」
「nums[k] までを使って、すべての長さ3のシーケンスを考えたときに、そのシーケンスの一番お尻の最小値」
……
というものです。これは昇順に並んでいるはずで、nums[k + 1] を使って、これを更新することは可能ですね。
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        inf = math.inf
        tail_nums = [inf] * len(nums)
        for num in nums:
            left = 0
            right = len(nums) - 1
            while left < right:
                middle = (left + right) // 2
                if tail_nums[middle] == num:
                    break
                if num < tail_nums[middle]:
                    right = middle
                    continue
                left = middle + 1
            else:
                tail_nums[right] = num

        len_subsequence = 0
        while len_subsequence < len(tail_nums) and tail_nums[len_subsequence] < inf:
            len_subsequence += 1
        return len_subsequence
```
