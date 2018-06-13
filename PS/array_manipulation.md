# Problem
https://www.hackerrank.com/challenges/crush/problem

# Solution

brute-force한 방법으로 배열에 일일히 값들을 더해주다보면, n이 매우 클 경우(10^7) timeout이 난다.<br/>
이 문제의 목적은 maximum acculmulated value를 찾는 것이므로 다음과 같이 해결할 수 있다.
```java
long getMaxInManipulatedArray(int n, int[][] queries) {
  int arr = new int[n + 1];
  for(int[] query : queries) {
    int startIndex = query[0] - 1;
    int endIndex = query[1];
    int value = query[2];
    arr[startIndex] += value;
    arr[endIndex -= value;
  }
  
  int max = 0;
  int tmp = 0;
  for(int value : arr) {
    tmp += value;
    max = Math.max(tmp, max);
  }
  return max;
}
```

Time complexity: O(n)<br/>
Space complexity: O(n)
