# 1st
- `can_be_broken[i]`は1-indexedでi番目の文字まで分割できるかどうかを表している
- wordBrakeというタイトル名だったから`can_be_broken`という変数名にしたが、あんまりよくないかも
- `i, j`はあまりよくないかも`end, start`とかにしてもよいかも
```py
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        wordSet = set(wordDict)
        can_be_broken = [False] * (len(s) + 1)
        can_be_broken[0] = True
        for i in range(1, len(can_be_broken)):
            for j in range(0, i):
                if can_be_broken[j] and s[j: i] in wordSet:
                    can_be_broken[i] = True
        return can_be_broken[-1]
```

# 2nd
## 1-indexed
- `can_be_segmented`に変数名を変更
```py
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        word_set = set(wordDict)
        can_be_segmented = [False] * (len(s) + 1)
        can_be_segmented[0] = True
        for end in range(1, len(can_be_segmented)):
            for start in range(end):
                if can_be_segmented[start] and s[start: end] in word_set:
                    can_be_segmented[end] = True
        return can_be_segmented[-1]
```
## 0-indexed
- `s[:end + 1]`が`word_set`に入っている場合を特別扱いする必要があるので1-indexedのほうが良いかも
```py
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        word_set = set(wordDict)
        can_be_segmented = [False] * len(s)
        for end in range(len(can_be_segmented)):
            if s[:end + 1] in word_set:
                can_be_segmented[end] = True
                continue
            for start in range(end):
                if can_be_segmented[start] and s[start + 1 : end + 1] in word_set:
                    can_be_segmented[end] = True
        return can_be_segmented[-1]
```
# 3rd
```py
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        word_set = set(wordDict)
        can_be_segmented = [False] * (len(s) + 1)
        can_be_segmented[0] = True
        for end in range(1, len(can_be_segmented)):
            for start in range(end):
                if can_be_segmented[start] and s[start: end] in word_set:
                    can_be_segmented[end] = True
        return can_be_segmented[-1]
```
