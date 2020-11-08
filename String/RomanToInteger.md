# 13. Roman to Integer

## Description
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M
```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.

**Example 1**
```
Input: s = "III"
Output: 3
```

**Example 2**
```
Input: s = "IV"
Output: 4
```
**Example 3**
```
Input: s = "IX"
Output: 9
```
## Solution
```python
def romanToInt(self, s: str) -> int:
    roman = {"I": 1,"V":5,"X":10,"L":50,"C":100,"D":500,"M":1000}
    number = 0
    index = 0
    while index < len(s):
        if index + 1 < len(s) and roman[s[index]] < roman[s[index+1]]:
            number -= roman[s[index]]
        else:
            number += roman[s[index]]
        index += 1
    return number
```

## Problem Analysis
In this problem, we may noticed for the roman string, we may build a dictionary to store all the roman to integer pairs. In general cases, we just need to iterate every character from "s" and find the corresponding interger from this dictionary and add this number to the final number. For the unusual cases, for example, "I" before "X", we need to subtract "I" which is 1 first and add "X" which is 10 to the final number. In this approach, every character only need to be traced once, the time complexity is O(n) then and no extra memory space leads to space complexity to be O(1).
