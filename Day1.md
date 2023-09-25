# Day1 | Array 1 | 704 Binary Search，27 Remove Element

## Today's reading list
https://programmercarl.com/%E6%95%B0%E7%BB%84%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html

https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html

https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html

https://www.bilibili.com/video/BV12A4y1Z7LP

## 704
Two ways, [left, right] and [left, right) 

1. [left, right]：(Perfer this way)

```python 
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while (left <= right):
            middle = int((left + right) / 2)
            if target < nums[middle]:
                right = middle - 1
            elif target > nums[middle]:
                left = middle + 1
            else:
                return middle
        return -1
```
2. [left, right)：

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)
        while (left < right):
            middle = int((left + right) / 2)
            if target < nums[middle]:
                right = middle
            elif target > nums[middle]:
                left = middle + 1
            else:
                return middle
        return -1
```

Time complexity is O(log n)

Space complexity is O(1)

## 27
1. Burte force

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        ct, le = 0, len(nums)
        while (ct < le):
            if (nums[ct] == val):
                for i in range(ct + 1, le):
                    nums[i - 1] = nums[i]
                ct -= 1
                le -= 1
            ct += 1
        return ct
```

Time complexity is O(n^2)

Since we have to move the elements after the target element to the left, which is O(n), and we have to do this for n times, so the time complexity is O(n^2)

This is because the memory address of the elements in the array is continuous, we can't delete some element in the array, we can only overwrite it. In this case, we move the elements after the target element to the left by one position.

2. Two pointers

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow = 0
        for fast in range(len(nums)):
            if (nums[fast] != val):
                nums[slow] = nums[fast]
                slow += 1
        return slow
```
Time complexity is O(n)

Space complexity is O(1)

## Conclusion
1. Leanred how to use two pointers to solve the problems
2. Learned the essenstials of array
3. Reviewed the binary search algorithm
4. Total learning time: 3 hours