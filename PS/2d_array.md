# Problem
https://www.hackerrank.com/challenges/2d-array/problem

# Solution
```java
int hourglassSum(int[][] arr) {
    int maxSum = Integer.MIN_VALUE;
    int rowNum = arr.length;
    int colNum = arr[0].length;
    for(int row = 0; row < rowNum - 2; ++row) {
        for(int col = 0; col < colNum - 2; ++col) {
            int topSum = arr[row][col] + arr[row][col + 1] + arr[row][col + 2];
            int mid = arr[row + 1][col + 1];
            int bottomSum = arr[row + 2][col] + arr[row + 2][col + 1] + arr[row + 2][col + 2];

            maxSum = Math.max(maxSum, topSum + mid + bottomSum);
        }
    }
    return maxSum;
}
```

Time complexity: O(N^2)<br/>
Space complexity: O(1)
