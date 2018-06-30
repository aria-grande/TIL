# Problem
https://www.hackerrank.com/challenges/flipping-bits/problem

```
You will be given a list of 32 bit unsigned integers. 
Flip all the bits (1->0 and 0->1) and print the result as an unsigned integer.
```

# Solution
[bitwise를 operation](https://en.wikipedia.org/wiki/Bitwise_operation#NOT)을 이용하면 된다.
java에서 선언하는 int, long은 signed type이다.<br/>
[2의 보수](https://en.wikipedia.org/wiki/Two%27s_complement) 규칙에 따라 [MSB](https://ko.wikipedia.org/wiki/%EC%B5%9C%EC%83%81%EC%9C%84_%EB%B9%84%ED%8A%B8)가 0이면 양수, 1이면 음수를 의미한다.<br/>
```
 0 = 0000 ... 0000
-1 = 1111 ... 1111
```

변형 전 숫자의 [MSB(Most Significant Bit)](https://ko.wikipedia.org/wiki/%EC%B5%9C%EC%83%81%EC%9C%84_%EB%B9%84%ED%8A%B8)가 0일 경우, 변형 후에는 1이 될 것이며 음수로 취급될 것이다.<br/>
constraints에 따라 입력 값은 0 이상 2^32 미만이니, MSB는 항상 0임을 보증한다.<br/>
signed -> unsigned로 변형하기 위해 2^31을 더해줘야 하며, MSB의 1은 2^31을 의미하므로 한 번 더 더해줘야 한다.<br/>
로직을 정리하면 아래와 같다.

```java
long flippingBits(long N) {
  return ~N + (long) Math.pow(2, 31) * 2;
}
```

Time complexity: O(1)<br/>
Space complexity: O(1)
