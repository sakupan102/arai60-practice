# 1st
- プッシュダウンオートマトンに関する問題
    - 文法規則
      - S -> (S)
      - S -> {S}
      - S -> [S]
      - S -> 
    - でこの文法規則から作られる文脈自由言語を認識するプッシュダウンオートマトンを作ろうという話
    - 間違ってたらすみません
- https://github.com/rm3as/code_interview/pull/4/files#r1563812410
    - open_bracketsをappendした後はcontinueしてelseを消した方がいいかも
```python
class Solution:
    def isValid(self, s: str) -> bool:
        open_to_close = {"(": ")", "[": "]", "{": "}"}
        brackets_stack = []
        for char in s:
            if char in open_to_close.keys():
                brackets_stack.append(char)
            else:
                if not len(brackets_stack) > 0:
                    return False
                open_brackets = brackets_stack.pop()
                if open_to_close[open_brackets] != char:
                    return False
        if len(brackets_stack) > 0:
            return False
        return True
```
# 2nd
- stackが空であるかをlenを使って判断するのではなく、真理値を用いた
- open_to_closeはプロパティごとに改行した方がいいかも
```python
class Solution:
    def isValid(self, s: str) -> bool:
        open_to_close = {"(": ")", "[": "]", "{": "}"}
        brackets_stack = []
        for char in s:
            if char in open_to_close:
                brackets_stack.append(char)
                continue
            if not brackets_stack:
                return False
            open_brackets = brackets_stack.pop()
            if open_to_close[open_brackets] != char:
                return False
        return not brackets_stack
```
# 3rd 
```python
class Solution:
    def isValid(self, s: str) -> bool:
        open_to_close = {
            "(": ")",
            "{": "}",
            "[": "]"
        }
        brackets_stack = []
        for char in s:
            if char in open_to_close:
                brackets_stack.append(char)
                continue
            if not brackets_stack:
                return False
            open_brackets = brackets_stack.pop()
            if open_to_close[open_brackets] != char:
                return False
        return not brackets_stack
```