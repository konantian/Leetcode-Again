# 118. Pascal's Triangle

## Description
Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

**Example 1**
```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```
## Solution
### Python
```python
def generate(self, numRows: int) -> List[List[int]]:
  if numRows == 0: return []
      if numRows == 1: return [[1]]

      base = [[1],[1,1]]
      if numRows == 2: return base

      for i in range(2,numRows):
          row = [1]
          previous = base[i-1]
          for j in range(len(previous)-1):
              row.append(previous[j]+previous[j+1])
          row.append(1)
          base.append(row)
      return base
```

### Java
```java
public List<List<Integer>> generate(int numRows) {
    List<List<Integer>> base = new ArrayList<List<Integer>>();
    if(numRows == 0) return base;

    base.add(new ArrayList<>());
    base.get(0).add(1);
    if(numRows == 1) return base;
    base.add(new ArrayList<>());
    base.get(1).add(1);
    base.get(1).add(1);
    for(int i = 2;i < numRows;i++){
        List<Integer> row = new ArrayList<>();
        List<Integer> previous = base.get(i-1);
        row.add(1);
        for(int j = 0;j<previous.size()-1;j++){
            row.add(previous.get(j)+previous.get(j+1));
        }
        row.add(1);
        base.add(row);
    }
    return base;
}    
```

## Problem Analysis
Based on the defination of Pascal's Triangle, each number is the numbers directly above it added together. In this case, we need to design the base case first.
We may consider three base cases here, when numRows = 0,1,2 and the corresponding triangle is [], [[1]],[[1,1]]. From these base cases, we may build more rows
base on them. In this problem, we are using two for loops, the outer foor loop is used to iterate every row starting from 2 to numRows. The inner loop is used to
sum each adjacent number above the current row to form the current row. It is not hard to see, the time complexity here is O(numRows * numRows) = O(n^2). Also,
the space complexity is O(n^2) because the more rows need to compute, more space we will need and we need to store every row in final solution.
