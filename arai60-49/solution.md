# 1st
```py
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        sorted_str_to_str_list = defaultdict(list)
        for string in strs:
            sorted_str = "".join(sorted(string))
            sorted_str_to_str_list[sorted_str].append(string)
        return sorted_str_to_str_list.values()
```
# 2nd 
- https://github.com/hayashi-ay/leetcode/pull/19/files
  - dict.values()はview objectをかえすのでlistに変換した方がよい。
```py
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        sorted_str_to_anagrams = defaultdict(list)
        for string in strs:
            sorted_str = "".join(sorted(string))
            sorted_str_to_anagrams[sorted_str].append(string)
        return list(sorted_str_to_anagrams.values())
```
# 3rd
```py
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        sorted_str_to_anagrams = defaultdict(list)
        for string in strs:
            sorted_str = "".join(sorted(string))
            sorted_str_to_anagrams[sorted_str].append(string)
        return list(sorted_str_to_anagrams.values())
```