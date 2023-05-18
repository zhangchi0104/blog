---
slug: leetcode-2130
description: Middle
image: cover.png
tags: 
  - leetcode
  - 刷题
title: LeetCode-2130
---
# LeetCode-2130

##  核心思路
1. 利用tow pointer (fast/slow) 来寻找中点。
	1.  fast pointer 每次forward两个node
2. 找到中点后翻转任意半条list，同时forward两个pointer求每对pair的和。取最大值

## 代码
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def pairSum(self, head: Optional[ListNode]) -> int:
        fast = slow = head
        prev = None
        slow_next = None
        # Progress forward (2 nodes each iter)
        # So when it reaches the end, the slow
        # pointer is in the middle of the kist 
        while fast and fast.next:
            fast = fast.next.next
            ## Each time slow proceeds,
            # reverse the connection
            # 5->4 become 4->5
            slow_next = slow.next 
            slow.next = prev
            prev = slow
            slow = slow_next 
        right = slow
        left = prev
        ans = 0
        # traverse through 2 partitions
        # compute sum for each pair
        while right:
            left_val = left.val
            right_val = right.val
            tmp = left_val + right_val
            if tmp > ans: ans = tmp
            left = left.next
            right = right.next
        return ans
```
