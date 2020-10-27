# 1.Two Sum

## Description
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

**Example 1:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```
**Example 2:**
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```
**Example 3:**
```
Input: nums = [3,3], target = 6
Output: [0,1]
```

## Solution
### Brute Force
#### python
```Python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    for i in range(len(nums)):
        for j in range(1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i,j]
```
#### Java
```java
public int[] twoSum(int[] nums, int target) {
    for(int i = 0;i<nums.length;i++){
        for(int j = i + 1;j<nums.length;j++){
            if(nums[i] + nums[j] == target){
                return new int[] {i,j};
            }
        }
    }
}
```

### One-pass Hash Table
#### Python
```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
        
    numsDict = {}
    for i,num in enumerate(nums):
        if target - num in numsDict:
            return [numsDict[target-num], i]
        numsDict[num] = i
```

#### Java
```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for(int i = 0;i<nums.length;i++){
        if(map.containsKey(target - nums[i])){
            return new int[] {map.get(target-nums[i]),i};
        }else{
            map.put(nums[i],i);
        }
    }
}
```

## Problem Analysis

For this problem, we may noticed we have to find for each num in nums, if there is a complement number in nums that has sum equals to target. On the other hand, we may consider the complement as *target - num*. In this case, we have to find out the index of *target - num* in nums. We have two choices here, the first is using a for loop to iterate nums and find out the index of *target - num*. Or, we can use hash table(Dictionary in Python, HashMap in Java) to store the num and index pair. In first choice, the time complexity to get the index is <img src="https://render.githubusercontent.com/render/math?math=O(n^2)"> because we have to iterate every number in nums. For the second approach, the time complexity is <img src="https://render.githubusercontent.com/render/math?math=O(1)">  which is much faster than the first approach. To sum up, the first approach has time complexity <img src="https://render.githubusercontent.com/render/math?math=O(n^2)"> , space complexity <img src="https://render.githubusercontent.com/render/math?math=O(1)"> . Compare to first approach, the second approach has time complexity <img src="https://render.githubusercontent.com/render/math?math=O(n)">  because we only need to iterate nums once. And space complexity here is <img src="https://render.githubusercontent.com/render/math?math=O(n)">  as well.The most important thing we learn from this problem is that we cannot have fastest algorithm with least memory usage at the same time. In most of the time, we consider the running time more important than the space. To reduce the time complexity, we may achieve this by increasing the space complexity.
