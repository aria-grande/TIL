# PROBLEM
https://leetcode.com/problems/toeplitz-matrix/

# SOLUTION
```java
class Solution {
    public boolean isToeplitzMatrix(int[][] matrix) {
        final int COL = matrix[0].length;
        for(int r = 0; r < matrix.length - 1; ++r){
            for(int c = 0; c < COL - 1; ++c){
                if(matrix[r][c] != matrix[r + 1][c + 1]) {
                    return false;
                }
            }
        }
        return true;
    }
}
```

time complexity: O(N*M)

space complexity: O(1)
