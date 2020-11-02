# 53. Maximum Subarray

## Description
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example 1**
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
**Example 2**
```
Input: nums = [1]
Output: 1
```

## Solution
### Greedy
```python
def maxSubArray(self, nums: List[int]) -> int:
    if len(nums) == 1: return nums[0]
    maximumTotal = nums[0]
    maximumSofar = nums[0]
    for i in range(1,len(nums)):
        maximumSofar = max(maximumSofar + nums[i], nums[i])
        maximumTotal  = max(maximumTotal, maximumSofar)
    return maximumTotal
```
```java
public int maxSubArray(int[] nums) {
    int maximumSofar = nums[0];
    int maximumTotal = nums[0];
    for(int i = 1;i<nums.length;i++){
        maximumSofar = Math.max(nums[i],maximumSofar+nums[i]);
        maximumTotal = Math.max(maximumSofar, maximumTotal);
    }
    return maximumTotal;
}
```
### Dynamic Programming
```python
def maxSubArray(self, nums: List[int]) -> int:
    dp = [nums[0]]
    maximumSum = nums[0]
    for i in range(1,len(nums)):
        dp.append(max(nums[i],dp[i-1] + nums[i]))
        maximumSum = max(maximumSum, dp[i])
    return maximumSum
```
```java
public int maxSubArray(int[] nums) {
    int dp[] = new int[nums.length];
    dp[0] = nums[0];
    int maximumTotal = nums[0];
    for(int i = 1;i<nums.length;i++){
        dp[i] = Math.max(dp[i-1] + nums[i],nums[i]);
        maximumTotal = Math.max(dp[i],maximumTotal);
    }
    return maximumTotal;
}
```

## Problem Analysis
In this problem, we need to track the local and global maximum sum at the same time. The local maximum is the maximum subarray sum from nums[0] to nums[i]. We need to keep comparing the local and global sum, for each iteration, if local maximum greater than the global maximum, we update the value of maximum sum. Because we only iterate nums once, the time complexity is O(n). The space complexity for greedy is O(1) and for DP is O(n).