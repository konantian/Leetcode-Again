# 26. Remove Duplicates from Sorted Array


## Description
Given a sorted array nums, remove the duplicates in-place such that each element appears only once and returns the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means a modification to the input array will be known to the caller as well.

**Example 1:**
```
Input: nums = [1,1,2]
Output: 2, nums = [1,2]
Explanation: Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the returned length.
```
**Example 2:**
```
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4]
Explanation: Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively. It doesn't matter what values are set beyond the returned length.
```

## Solution
### Two pointers
#### python
```python
def removeDuplicates(self, nums: List[int]) -> int:
    if(len(nums) <= 1) return len(nums)
    index = 0
    seen = None
    for i in range(len(nums)):
        if nums[i] != seen:
            seen = nums[i]
            nums[index] = nums[i]
            index += 1
    return index
```
#### Java
```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int i = 0;
    for (int j = 1; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
}
```

## Problem Analysis
Since the array is already sorted, we can keep two pointers i and j, where i is the slow-runner while j is the fast-runner. As long as nums[i] = nums[j], we increment j to skip the duplicate.When we encounter nums[j] != nums[i] the duplicate run has ended so we must copy its value to nums[i+1]. i is then incremented and we repeat the same process again until j reaches the end of array. Since we only iterate the arary once and not using extra space, the time complexity is O(n) and space complexity is O(1).