# 1st
- `for i in range(len(s)):`の部分はenumerateを使ってもよかったかも
```py
from collections import defaultdict
class Solution:
    def firstUniqChar(self, s: str) -> int:
        char_to_count = defaultdict(int)
        for char in s:
            char_to_count[char] += 1
        for i in range(len(s)):
            if char_to_count[s[i]] == 1:
                return i
        return -1
```
# 2nd 
- https://discord.com/channels/1084280443945353267/1195700948786491403/1231538588529852426
  - pythonのdictには順序がある
```py
from collections import defaultdict
class Solution:
    def firstUniqChar(self, s: str) -> int:
        char_to_count = defaultdict(int)
        for char in s:
            char_to_count[char] += 1
        for index, char in enumerate(s):
            if char_to_count[char] == 1:
                return index
        return -1
```
# 3rd
```py
from collections import defaultdict
class Solution:
    def firstUniqChar(self, s: str) -> int:
        char_to_count = defaultdict(int)
        for char in s:
            char_to_count[char] += 1
        for index, char in enumerate(s):
            if char_to_count[char] == 1:
                return index
        return -1
```