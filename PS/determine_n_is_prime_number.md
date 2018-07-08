# Problem
https://www.hackerrank.com/challenges/ctci-big-o/editorial?h_l=playlist&slugs%5B%5D=interview&slugs%5B%5D=interview-preparation-kit&slugs%5B%5D=miscellaneous

```
For a given integer n, determine if n is prime number or not.
You should determine in O(n^(1/2))) time complexity!
```
# Solution
**time complexity가 O(n^(1/2))가 되기 위해서는 sqrt(n) 값을 이용**해야 한다.<br/>
n이 3 이상일 경우, n이 2부터 int(sqrt(n))의 값으로 나눠지지 않으면 소수이다.

성립하는 이유는 다음의 예를 보면 안다.<br/>
sqrt(5) = 2.xx => 2<br/>
ㄴ 5는 2로 나눠지지 않으므로 소수이다.<br/>
sqrt(6) = 2.xx => 2<br/>
ㄴ 6은 2로 나눠지므로 소수가 아니다.<br/>
sqrt(10) = 3.xx => 3<br/>
ㄴ 1-은 2~3 중 2로 나눠지므로 소수가 아니다.<br/>

```java
boolean isPrime(int n) {
  if(n == 1) {
    return false;
  }
  if(n == 2) {
    return true;
  }
  for(int i = 2; i <= Math.sqrt(n); ++i) {
    if(n % i == 0) {
      return false;
    }
  }
  return true;
}
```

Time complexity: O(n^(1/2))<br/>
Space complexity: O(1)
