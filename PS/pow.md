# Problem
```
양수 n이 주어질 때, 2의 n승 값을 구하는 메소드를 작성하라.
```

# Solution
## 무식한 방법 1
```java
BigInteger exponential(int n) {
  if(n == 0) {
    return BigInteger.ONE;
  }
  if(n == 1) {
    return new BigInteger("2");
  }
  return 2 * exponential(n - 1);
}
```
-> stack overflow나기 딱 좋다;;

## 괜찮은 솔루션
```java
BigInteger exponential(int n) {
  if(n == 0) {
    return BigInteger.ONE;
  }
  if(n == 1) {
    return new BigInteger("2");
  }
  BigInteger val = exponential(n / 2);
  BigInteger newVal = val.multiply(val);
  if(n % 2 != 0) {
    newVal = newVal.multiply(new BigInteger("2"));
  }
  return newVal;
}
```

Time complexity: O(log n)<br/>
Space complexity: O(1) // 재귀에 의한 stack space도 고려한다면 O(log n)
