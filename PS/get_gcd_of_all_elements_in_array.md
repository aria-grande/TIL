# Problem
For a given integer array, get the greatest common denominator of all elements.

# Solution
`GCD(a, b, c) = GCD(GCD(a, b), c)`에 기반한 알고리즘이다.

```java
int getGCDOfAll(int[] arr) {
    int result = arr[0];
    for(int i = 1; i < arr.length; ++i) {
      result = getGCD(arr[i], result);
    }
    return result;
}
int getGCD(int a, int b) {
  if(b == 0) {
    return a;
  }
  return getGCD(b, a % b);
}
```
Time complexity: O(N)<br/>
Space complexity: O(1)
