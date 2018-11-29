# Problem
https://leetcode.com/problems/factorial-trailing-zeroes/

```
Given an integer n, return the number of trailing zeroes in n!.
```

# Solution
Trailing zero라는건 10일때 1개이며, 2와 5의 한 쌍으로 구성될 수 있다.

n이 5로 나뉘어지면, 그 몫이 n~ n/5까지의 trailing zero의 count가 된다.

10을 예로 들어보자.

`10! = 10 * 9 * 8 * 7 * 6 * 5 * 4 * 3 * 2 * 1`

trailing zeroes는 (10), (5, 2) 총 두 개이다.

10을 5로 나눠보면 그 몫은 2고, 이 때, 10과 5를 커버하게 된다. 

고로 그 다음 4!부터 다시 (2,5) 혹은 (10)을 찾는 과정을 진행하면 된다.

**5를 찾았으니 2도 찾아야 하는 거 아니야?** 라고 생각할 수 있겠지만, 

5만 찾으면 2는 5보다 작으므로 n/5~n 내에서 이미 찾아지게 된다.

```java
public int trailingZeroes(int n) {
  int count = 0;
  while(n > 0) {
    n /= 5;
    count += n;
  }
  return count;
}
```

Time complexity: O(log5 N)

Space complexity: O(1)
