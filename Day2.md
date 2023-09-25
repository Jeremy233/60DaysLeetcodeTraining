# Day2 | Array 2 | 977 Squares of a Sorted Array, 209 Minimum Size Subarray Sum, 59 Spiral Matrix II

## Today's reading list
https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

https://www.bilibili.com/video/BV1tZ4y1q7XE/?t=1&spm_id_from=333.1007.seo_video.first&vd_source=fb9e07202b23bd78e8ec7259de6f00bb

https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html

https://programmercarl.com/%E6%95%B0%E7%BB%84%E6%80%BB%E7%BB%93%E7%AF%87.html#%E6%95%B0%E7%BB%84%E7%9A%84%E7%BB%8F%E5%85%B8%E9%A2%98%E7%9B%AE

## 977 Squares of a Sorted Array

*First thought is to use brute force:*

**1. Brute force**

which is calculate the squares of each element in the array, and then sort the array. Which means the time complexity is O(n) + O(nlogn) = O(nlogn)

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        nums = [i ** 2 for i in nums]
        return sorted(nums)
```

*Then I check the link above and find we can use two pointers to solve this problem.*

**2. Two pointers**
* Since the array is sorted, the negative value will probably become the largest, so the largest value of the array will either be on the left or on the right.
* So we can use two pointers, i and j, i will points to the starting position and j will points to the ending position.
* Define a new array, the size is the same as the original array, and the index k will points to the end of the array. 
* For example, if the input array is [-4, -1, 0, 3, 10], then the i will points to -4, j will points to 10, and k equals to 4. Then we compare the squared value of -4 and 10, and put the larger one into the new array.
* In this case, we put 100(10^2) at newarray[k], and update k and j, then we continue to compare the squared value that i and j pointed to. until the new array is full. 

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        k = len(nums) - 1
        new_nums = [0] * len(nums)
        i, j = 0, len(nums) - 1
        while (i <= j):
            if (nums[i] ** 2 < nums[j] ** 2):
                new_nums[k] = nums[j] ** 2
                j -= 1
            else:
                new_nums[k] = nums[i] ** 2
                i += 1
            k -= 1
        return new_nums
```
In this case, the time complexity is O(n), since we don't need to sort the array. 

## 209 Minimum Size Subarray Sum

*Fisrt, I think I can use the two pointers, where we have i and j, i will keep looping through the array, and j will be update only the sum of elements that i looped is greater or equal to target.*

*Then I can write the code of this thought:*
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        if (sum(nums) < target):
            return 0
        else: 
            i, j, temp_sum, temp_len = 0, 0, 0, len(nums)
            for i in range(len(nums)):
                temp_sum += nums[i]
                if (temp_sum >= target):
                    if (temp_len > i - j + 1):
                        temp_len = i - j + 1
                    j = i + 1
                    temp_sum = 0
            return temp_len

```
However, this code only passed 12/21 test cases. So check the link above. 

**Still, we use two pointers method, or in this problem, called slide window**

#### Slide window

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left, right = 0, 0
        l = len(nums)
        min_len = float('inf')
        current_sum = 0
        while right < l:
            current_sum += nums[right]
            while current_sum >= target:
                min_len = min(min_len, right - left + 1)
                current_sum -= nums[left]
                left += 1
            right += 1
        if min_len != float('inf'):
            return min_len
        else:
            return 0
```

So in my solution, the if should be changed to while. 

## 59 Spiral Matrix II

Don't have any idea about this problem, so check the link above. 

This problem is still binary search, but it's a little bit different from the previous one. 

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        nums = [[0] * n for _ in range(n)]
        startx, starty = 0, 0
        loop, mid = n // 2, n // 2
        count = 1
        for offset in range(1, loop + 1):
            for i in range(starty, n - offset):
                nums[startx][i] = count
                count += 1
            for i in range(startx, n - offset):
                nums[i][n - offset] = count
                count += 1
            for i in range(n - offset, starty, -1):
                nums[n - offset][i] = count
                count += 1
            for i in range(n - offset, startx, -1):
                nums[i][starty] = count
                count += 1
            startx += 1
            starty += 1
        if (n % 2 != 0):
            nums[mid][mid] = count;
        return nums
```
Here is the solution

## Conclusion
1. Getting familiar with the two pointers method
2. Total learning time: 3 hours