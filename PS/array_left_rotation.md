# Problem
https://www.hackerrank.com/challenges/array-left-rotation/problem
```
정수를 담고 있는 배열 arr와 회전 횟수 rotateCount이 주어졌을 때, arr를 rotateCount번 왼쪽으로 회전 시켜라.
```

# Solution

```java
int[] rotate(int[] arr, int rotateCount) {
  final int len = arr.length;
  int[] rotated = new int[len];
 
  for(int i = 0; i < len; ++i) {
    rotated[i] = arr[(rotateCount + i) % len];
  }
  return rotated;
}
```
N이 배열의 길이일 때,<br/>
Time complexity: O(n)<br/>
Space complexity: O(n)
