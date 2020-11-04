# 66. Plus One

## Description
Given a non-empty array of digits representing a non-negative integer, increment one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contains a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

**Example 1**
```
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

**Example 2**
```
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```

## Solution
### Python
```python
def plusOne(self, digits: List[int]) -> List[int]:
    promo = 1
    for i in reversed(range(len(digits))):
        if digits[i] + promo == 10:
            digits[i] = 0
            promo = 1
        else:
            digits[i] += promo
            promo = 0

    if promo == 1:
        digits.insert(0,1)
    return digits
```

### Java
```java
public int[] plusOne(int[] digits) {
    int promo = 1;
    for(int i = digits.length - 1;i>-1;i--){
        if(digits[i] + promo == 10){
            digits[i] = 0;
            promo = 1;
        }else{
            digits[i] += promo;
            promo = 0;
        }
    }
    if(promo == 1){
        int[] output = new int[digits.length+1];
        output[0] = 1;
        return output;
    }else{
        return digits;
    }
}
```

## Problem Analysis
In this problem, every digit of the interger stored on every index of list - digts. To plus the number by one, we need to consider the case that digit equal to 9 and we will need a promotion in this case. We iterate digits from right to left and check if there is a dight equals to 9. Since we only iterate digits once, the time complexity if O(n) and we are not using extra memory space except the leading 1 in some corner cases, the space complexity is O(1).