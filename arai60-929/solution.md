# 1st
- 最初にlocal_nameとdomain_nameを分けてlocal_nameだけを処理していく。
- local_nameに関する処理は関数化して外に出してもいいかも。
- https://google.github.io/styleguide/pyguide.html#310-strings
  - 文字列を+=でつなぐ場合文字列の再構成が生じてO(n**2)の時間がかかる場合がある
  - Cpythonの場合最適化がかかるhttps://github.com/python/cpython/blob/bb3e0c240bc60fe08d332ff5955d54197f79751c/Objects/unicodeobject.c#L11768
  - 文字列をつなぐ時は`".".join()`を用いるのが良い
```py
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        unique_emails = set()
        for email in emails:
            unique_email = []
            local_name, domain_name = email.split("@")
            for char in local_name:
                if char == "+":
                    break
                if char == ".":
                    continue
                unique_email.append(char)
            unique_email.append("@")
            unique_email.append(domain_name)
            unique_email_string = "".join(unique_email)
            unique_emails.add(unique_email_string)
        return len(unique_emails)
```
# 2nd
- https://github.com/hayashi-ay/leetcode/pull/25/files
  - こちらを参考に文字列操作関数を用いた実装に変更した
- `ignored_local_name`と`filtered_local_name`はぱっと見では意味が伝わらないかも。(結局良い名前が思いつかなかったのでこのまま)
```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        unique_emails = set()
        for email in emails:
            local_name, domain_name = email.split("@")
            ignored_local_name = local_name.split("+")[0]
            filtered_local_name = ignored_local_name.replace(".", "")
            unique_emails.add(filtered_local_name + "@" + domain_name)
        return len(unique_emails)
```
# 3rd
```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        unique_emails = set()
        for email in emails:
            local_name, domain_name = email.split("@")
            removed_local_name = local_name.split("+")[0]
            replaced_local_name = removed_local_name.replace(".", "")
            unique_emails.add(replaced_local_name + "@" + domain_name)
        return len(unique_emails)
            
```