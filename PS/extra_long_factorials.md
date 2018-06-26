# Problem

https://www.hackerrank.com/challenges/extra-long-factorials/editorial

# Solution

```java
BigInteger factorial(int n) {
  BigInteger result = BigInteger.ONE;
  do {
    result = result.multiply(new BigInteger(String.valueOf(n));
  } while(n -- > 1);
  return result;
}
```

Time complexity: O(n)<br/>
Space complexity: O(1)
