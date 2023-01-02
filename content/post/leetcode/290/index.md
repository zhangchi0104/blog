---
slug: leetcode-290
description: Easy
image: cover.png
tags: 
  - leetcode
  - 刷题
title: Leetcode-290 (Word Pattern)
---
# Leetcode-290 (Word Pattern)


难度为easy, 也不用考虑什么算法，就一个for loop搞定。

## 核心思路
`pattern`中的字母与所提供的字符串`s` 中的单词为一一对应的关系，所以同是便利两个字符串即可，如果有与当前对应关系不匹配的单词，则提前返回`False`，否则则在便利完成后返回`True`即可。

##  踩坑
python `dict` 所表达的是many to one关系，即一个value可对应多个key。第一次提交时没有意识到这个问题， fail了一个test case。
```
Input:
    pattern = "abba"
    s = "dog dog dog dog"
Output: True
Expbected: False
```
解决的方法也很简单， 多添加一个 `set`用来记录已知单词，其实也可以用`mappings.values()`，不过会慢一点， 但是不需要额外的内存 （理论上讲）。

## 代码 (Python3)
```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        # 如果长度不匹配则提前返回 False
        if len(pattern) != s.count(" ") + 1: return False
        # 初始化数据结构用于表达one to one mapping
        mappings = {}
        known_words = set()
        # 同时便利pattern 和 s
        for word, label in zip(s.split(), pattern):
            known_word = mappings.get(label, None) 
            if not known_word:
                # 如果需要把新label分配给已知的单词
                # 提前返回False
                if word in known_words:
                    return False
                # 添加到mapping中
                mappings[label] = word
                known_words.add(word)
            # 不匹配则提前返回
            elif word != known_word:
                return False

        return True

```
 