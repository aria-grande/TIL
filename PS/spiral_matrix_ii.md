# Problem
https://leetcode.com/problems/spiral-matrix-ii/

```
Given a positive integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.
```

# Solution
```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] matrix = new int[n][n];
        int row = 0, col = 0, depth = 0;
        char way = 'r';
        for(int num = 1; num <= n * n; ++num) {
            matrix[row][col] = num;
            if(way == 'r') {
                if(col == n - 1 - depth) {
                    row++;
                    way = 'd';
                } else {
                    col++;
                }
            }
            else if(way == 'l') {
                if(col == depth) {
                    row--;
                    way = 'u';
                } else {
                    col--;
                }
            }
            else if(way == 'u') {
                if(row == 1 + depth) {
                    depth++;
                    col++;
                    way = 'r';
                } else {
                    row--;
                }
            }
            else if(row == n - 1 - depth) {
                col--;
                way = 'l';
            }
            else {
                row++;
            }
        }
        return matrix;
    }
}
```

Time complexity: O(N^2)

Space complexity: O(N^2)
