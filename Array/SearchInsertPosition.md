# 35. Search Insert Position

## Description
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

**Example 1**
```
Input: nums = [1,3,5,6], target = 5
Output: 2
```
**Example 2**
```
Input: nums = [1,3,5,6], target = 7
Output: 4
```
**Example 3**
```
Input: nums = [1,3,5,6], target = 0
Output: 0
```


## Solution
### Linear Search
```python
def searchInsert(self, nums: List[int], target: int) -> int:
    for i in range(len(nums)):
        if target <= nums[i]:
            return i
    return len(nums)
```
### Binary Search
#### Python
```python
def searchInsert(self, nums: List[int], target: int) -> int:
    i = 0
    j = len(nums) - 1
    if target > nums[-1]:
        return len(nums)
    elif target <= nums[0]:
        return 0
    else:
        while i <= j:
            middle = i + (j - i)//2
            if nums[middle] == target: return middle
            elif nums[middle] > target: j = middle-1
            elif nums[middle] < target: i = middle+1
    return i

```

#### Java
```java
public int searchInsert(int[] nums, int target) {
    int i = 0;
    int j = nums.length - 1;
    while (i <= j){
        int middle = i + (j - i) / 2;
        if(nums[middle] == target) return middle;
        else if(nums[middle] < target) i = middle + 1;
        else if(nums[middle] > target) j = middle - 1;
    }
    return i;
}
```

## Problem Analysis
The most straight approach is using linear search and compare every number in nums with target. If target smaller or equal to a number in nums, then just return this number's index as the solution. By this approach, the best case we only need to examine only a single number, but in the worst case, we have to iterate all the number in nums. So, the time complexity is O(n) and space complexity is O(1) because we are not using extra memory space to store data. To make improvement on this algorithm, we introduce binary search. We have two pointers i and j here and they are initialized to 0 and the last index of nums. For each iteration, we only check the number in the middle position of nums[i:j].If they are not equal, the half in which the target cannot lie is eliminated and the search continues on the remaining half, again taking the middle element to compare to the target value, and repeating this until the target value is found.  Hence, by each iteration, we reduce the search space by half. The time complexity is O(logn) and space complexity is O(1) as well.