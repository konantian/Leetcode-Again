# 27. Remove Element

## Description
Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means a modification to the input array will be known to the caller as well.

**Example 1:**
```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2]
Explanation: Your function should return length = 2, with the first two elements of nums being 2.
It doesn't matter what you leave beyond the returned length. For example if you return 2 with nums = [2,2,3,3] or nums = [2,3,0,0], your answer will be accepted.
```
**Example 2:**
```
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3]
Explanation: Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4. Note that the order of those five elements can be arbitrary. It doesn't matter what values are set beyond the returned length.
```

## Solution
### Two pointers
#### Python
```python
def removeElement(self, nums: List[int], val: int) -> int:
    index = 0
    for i in range(len(nums)):
        if nums[i] != val:
            nums[i],nums[index] = nums[index],nums[i]
            index += 1
    return index
```

### Two pointers with elements to remove are rare
#### Python
```python
def removeElement(self, nums: List[int], val: int) -> int:
    index = 0
    n = len(nums) - 1
    while index < len(nums):
        if nums[i] == val:
            nums[i] = nums[n]
            n -= 1
        else:
            index += 1

    return n
```

## Problem Analysis
For both approach, the average time complexity is both O(n), because we only iterate nums once. As for the space complexity, since we are not using extra space, the space complexity is always constant which is O(1). In this problem, the only difference between two approaches is how many times we need to remove a element. For the first approach, we reorder all the elements that are not equal to val to the front of the list and put all the elements equal to val to the end of the list. This solutoin does works, but not the best solution so far. Just consider the case that there is a list with n elements and only 1 elements equal to val and this element is the first element in this list. In this case, if we follow the first solution, we have to move n-1 elements to the beginning of the list which is unnecessary. To optimize the first solution, we now only swap the elements equal to val with the ending elements of the list.