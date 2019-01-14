# Problem
https://www.knowsh.com/Notes/250480/Active-And-Inactive-Cells-After-K-Days

(유사문제: https://www.geeksforgeeks.org/active-inactive-cells-k-days/)


# Solution
인접한 두 배열의 값이 같으면 0, 다르면 1.
XOR 연산이 필요한 problem 이다.

```java
public List<Integer> cellCompete(int[] states, int days) {
  int[] afterStates = new int[states.length];
  while(days-- > 0) {
    // XOR
    for(int i = 0; i < states.length; ++i) {
      int left = (i == 0) ? 0 : states[i - 1];
      int right = (i == states.length - 1) ? 0 : states[i + 1];
      afterStates[i] = left ^ right;
    }
    // Copy and reassign array
    for(int j = 0; j < states.length; ++j) {
      states[j] = afterStates[j];
    }
  }
  return Arrays.stream(afterStates).boxed().collect(Collectors.toList());
}
```
`states`의 길이를 N, `days`를 D라 할 때,

Time complexity: O(D * N)

Space complexity: O(N)
