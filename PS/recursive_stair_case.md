# Problem
https://www.hackerrank.com/challenges/ctci-recursive-staircase/problem
```
데이빗네 집에는 n 높이의 계단이 있다. 데이빗은 한번에 1, 2, 3개를 뛰어올라갈 수 있다.
이 때, 계단을 올라가는 방법의 가짓수를 구하는 메소드를 작성하라.
```
예) n = 3일 때, 방법은 4가지. (0 - 1 - 1 - 1) / (0 - 1 - 2) / (0 - 2 - 1) / (0 - 3)

# Solution
recursive한 방법으로 해결할 수 있다. 특정 계단을 밟고 올라가는 경우와 밟지 않고 올라가는 경우를 더해주면 된다.<br/>
n = 1일 때 1가지, n = 2일 때 2가지, n = 3일때 가지 이며, 그 이후는 ways(n) = ways(n - 1) + ways(n - 2) + ways(n - 3)으로 계산될 수 있다.
```java
int getNumberOfWaysToClimb(int n) {
  if (n <= 2) {
    return n;
  }
  if(n == 3) {
    return 4;
  }
  return getNumberOfWaysToClimb(n - 1) + getNumberOfWaysToClimb(n - 2) + getNumberOfWaysToClimb(n - 3);
}
```

이럴 경우, n의 크기가 커지면 어떻게 될까?<br/>
Stack overflow가 발생하거나 timeout 문제에 부딪힐 수 있다.<br/>
bottom-up 방식으로 구현해보자.

```java
int getNumberOfWaysToClimb(int n) {
  if (n <= 2) {
    return n;
  }
  if(n == 3) {
    return 4;
  }
  int[] ways = new int[n + 1];
  ways[1] = 1;
  ways[2] = 2;
  ways[3] = 4;
  for(int i = 4; i <= n; ++i) {
    ways[i] = ways[i - 1] + ways[i - 2] + ways[i - 3];
  }
  return ways[n];
}
```

Time complexity: O(n)<br/>
Space complexity: O(n)
