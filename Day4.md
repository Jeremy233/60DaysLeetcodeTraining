# Day4 | Linked List 2 | 24 Swap Nodes in Pairs, 19 Remove Nth Node From End of List

## Today's reading list
https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE






## 24 Swap Nodes in Pairs
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fake_head = ListNode(next=head)
        current = fake_head
        while current.next and current.next.next:
            temp = current.next
            temp1 = current.next.next.next

            current.next = current.next.next
            current.next.next = temp
            temp.next = temp
            temp.next = temp1
            current = current.next.next
        return fake_head.next
```

## 19 Remove Nth Node From End of List
```python