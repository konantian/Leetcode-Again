# 119. Pascal's Triangle II

## Description
Given an integer rowIndex, return the rowIndexth row of the Pascal's triangle.

Notice that the row index starts from 0.

**Example 1**
```
Input: rowIndex = 3
Output: [1,3,3,1]
```

**Example 2**
```
Input: rowIndex = 0
Output: [1]
```

**Example 3**
```
Input: rowIndex = 1
Output: [1,1]
```

## Solution
### Python
```python
def getRow(self, rowIndex: int) -> List[int]:
    base = [0]*(rowIndex+1)
    base[0] = 1
    for i in range(1,rowIndex+1):
        for j in range(i,0,-1):
            base[j] += base[j-1]
    return base
```
### Java
```java
public List<Integer> getRow(int rowIndex) {
    Integer[] res = new Integer[rowIndex+1];
    Arrays.fill(res,0);
    res[0] = 1;

    for(int i = 1; i <= rowIndex; i++){
        for(int j = i; j > 0; j--){
            res[j] = res[j] + res[j-1];
        }
    }

    return Arrays.asList(res);
}
```

### Problem Analysis
This problem looks very similar with problem 118. The only difference here is we only need to return the rowIndex row of Pascal's Triangle. The most
straight approach might come to the mind is to calculate all the rows starting from 1 to rowIndex and return the last row which is the rowIndex row. 
The only problem with this approach is we are introducing unnecessary space to store extra rows. The better approach is just store only single row and
this will be the final answer. The algorithm here is we first initialize an array with length equals to rowIndex+1, except the first number is 1, all
other number will be 0. We can see here that this is the base case when rowIndex = 0. To obtain the final answer, we need to use two for loops. The outer
for loop will be used to calculate for each row starting from 1 until the row is rowIndex. The inner for loop will be used to update the value for each row.
Based on the definition of Pascal's Triangle, to update current row, we need information from the previous row. So, in our inner for loop, because we
only store a single row in our array, we just keep updating this row until we get our expected answer.
