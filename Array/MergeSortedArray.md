# 88. Merge Sorted Array

## Description
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:

The number of elements initialized in nums1 and nums2 are m and n respectively.
You may assume that nums1 has enough space (size that is equal to m + n) to hold additional elements from nums2.

**Example 1**
```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## Solution
### Pyhon
```python
def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
    """
    Do not return anything, modify nums1 in-place instead.
    """
    p1 = m - 1
    p2 = n - 1
    # set pointer for nums1
    end = m + n - 1

    # while there are still elements to compare
    while p1 >= 0 and p2 >= 0:
        if nums1[p1] < nums2[p2]:
            nums1[end] = nums2[p2]
            p2 -= 1
        else:
            nums1[end] =  nums1[p1]
            p1 -= 1
        end -= 1

    # add missing elements from nums2
    nums1[:p2 + 1] = nums2[:p2 + 1]
```
### Java
```java
void merge(int A[], int m, int B[], int n) {
    int i=m-1;
    int j=n-1;
    int k = m+n-1;
    while(i >=0 && j>=0)
    {
        if(A[i] > B[j])
            A[k--] = A[i--];
        else
            A[k--] = B[j--];
    }
    while(j>=0)
        A[k--] = B[j--];
}
```

## Problem Analysis
For this problem, we hvae two directions to go. The first is append num2 to the ending of nums1 and using any sort algorithm you like to sort the combined array. By this approach, 
The time complexity will be O(nlogn) and the space complexity is O(1). In another direction, we may using three pointers to track the ending of nums1, nums2, and 
the last number in nums1. Instead of comparing element by elment from the beginning of two arrays, we start comparing from the ending of them. By this way,
we can fill all the empty space at the ending of nums1 by the elements either from nums1 itself or from nums2. At the end, we just need to replace the first part of nums1 
with the elements from nums2. In this way, the time complexity is O(n) and the space complexity is also O(1).
