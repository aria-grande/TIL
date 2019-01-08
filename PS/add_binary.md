# Problem
https://leetcode.com/problems/add-binary/
```
Given two binary strings, return their sum (also a binary string).

The input strings are both non-empty and contains only characters 1 or 0.
```

# Solution
주의1. sum은 1의 자리부터 해야 하므로 두 string의 last index부터 접근해야 한다.

주의2. `String a`와 `String b`는 다른 길이 일 수도, 같은 길이 일 수도 있다.

주의3. 넘어가는 수(`carry`)가 있을 수 있다.

주의4. a와 b에 대해 sum이 끝난 후, 남은 `carry`를 잊지 말자.

```java
public String addBinary(String a, String b) {
    char[] as = a.toCharArray();
    char[] bs = b.toCharArray();
    StringBuilder sb = new StringBuilder();

    int carry = 0;
    for(int i = 1; i <= Math.max(as.length, bs.length); ++i) {
        int ac = (as.length < i) ? 0 : Character.getNumericValue(as[as.length - i]);
        int bc = (bs.length < i) ? 0 : Character.getNumericValue(bs[bs.length - i]);
        int sum = ac + bc + carry;

        sb.insert(0, sum % 2);
        carry = sum / 2;
    }
    if(carry == 1) {
        sb.insert(0, carry);
    }

    return sb.toString();
}
```

Time complexity: O(N)

Space complexity: O(N)
