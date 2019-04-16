# Problem
https://leetcode.com/problems/ugly-number/

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.

# Solution

```java
public boolean isUgly(int num) {
  if(num <= 0) {
      return false;
  }
  while(num % 2 == 0) {
      num /= 2;
  }
  while(num % 3 == 0) {
      num /= 3;
  }
  while(num % 5 == 0) {
      num /= 5;
  }
  return num == 1;
}
```

Time complexity: O(N)

Space complexity: O(1)

# 회고
num을 2로 안나눠질 때까지 2로 나누고, 3으로, 5로, ... 하는 과정이 비효율 적이라 생각해서, log를 이용해서 2로 나눠지는 몫을 찾고 하여 time complexity를 조금 더 줄여보고자 했었다. 
하지만 log2(num)은 사용할 수 없다. 예를 들어 log2(12)는 3.xx이고, 이를 int로 형변환 하여 다시 곱하면 2^3 = 8인데, 12 % 8은 0이 아니므로, 2로 나눠질 수 없는 넘버라 하여 false를 리턴하는 로직을 짰기 때문이다.
하지만 실제로 12는 2*2*3으로 2는 3개가 아니라 2개까지만 곱해지는 ugly number이다. 따라서 log를 쓸 수 없음이 증명되어, brute force한 방법으로 진행했다.
