# Problem
rotate a 2d integer array in right.

# Solution
```java
void rotate(int[][] arr) {
  final int LAST = arr.length - 1;
  for(int d = 0; d < arr.length / 2; ++d) {
    for(int i = d; i < LAST - d; ++i) {
      int temp = arr[d][i];
      arr[d][i] = arr[LAST - i][d];
      arr[LAST - i][d] = arr[LAST - d][LAST - i];
      arr[LAST - d][LAST - i] = arr[i][LAST - d];
      arr[i][LAST - d] = temp;
    }
  }
}
```
Time complexity: O(N^2)

Space complexity: O(1)
