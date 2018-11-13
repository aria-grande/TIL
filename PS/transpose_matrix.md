# Problem
https://leetcode.com/problems/transpose-matrix/
```
Given a matrix A, return the transpose of A.

The transpose of a matrix is the matrix flipped over it's main diagonal, 
switching the row and column indices of the matrix.
```

# Solution
```java 
public int[][] transpose(int[][] A) {
    final int ROW = A.length;
    final int COL = A[0].length;
    int[][] result = new int[COL][ROW];
    
    for(int r = 0; r < ROW; ++r) {
        for(int c = 0; c < COL; ++c) {
            result[c][r] = A[r][c];
        }
    }
    return result;
}
```

Time complexity: O(ROW * COL)

Space complexity: O(ROW * COL)
