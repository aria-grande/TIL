# Problem
```
Given a 2D matrix matrix, find the sum of the elements 
inside the rectangle defined by its upper left corner (row1, col1) and 
lower right corner (row2, col2).

1. You may assume that the matrix does not change.
2. There are many calls to sumRegion function.
3. You may assume that row1 ≤ row2 and col1 ≤ col2.
```

https://leetcode.com/problems/range-sum-query-2d-immutable/

# Solution
Brute-force 하게 풀었더니, `sumRegion`을 많이 호출하니 Time Limit Exceeded Error가 발생했다.
최적화 할 수 있는 방법은 무엇일까?

## DP 스럽게 푸는 것
- (0,0)부터 (n, m)까지의 누적 summation 영역 값을 `acc`(accumulation)에 담아 보자.
- (row1, col1) ~ (row2, col2) 까지의 summation은 `acc[row2 + 1][col2 + 1] - acc[row1][col2 + 1] - acc[row2 + 1][col1] + acc[row1][col1]` 과 같다.

```java
class NumMatrix {
  private int[][] acc;
  public NumMatrix(int[][] matrix) {
    if(matrix.length == 0 || matrix[0].length == 0) {
      return ;
    }
    
    this.acc = new int[matrix.length + 1][matrix[0].length + 1];
    for(int row = 0; row < matrix.length; ++row) {
      for(int col = 0; col < matrix[0].length; ++col) {
        acc[row + 1][col + 1] = acc[row][col + 1] + acc[row + 1][col] - acc[row][col] + matrix[row][col];
      }
    }
  }

  public int sumRegion(int row1, int col1, int row2, int col2) {
    return acc[row2 + 1][col2 + 1] - acc[row1][col2 + 1] - acc[row2 + 1][col1] + acc[row1][col1];
  }
}

```
N이 row의 길이, M이 column의 길이일 때,

Time complexity: O(N*M)

Space complexity: O(N*M)
