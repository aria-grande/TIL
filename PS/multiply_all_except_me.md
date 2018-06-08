# Problem
```
정수로 된 배열이 주어지면, 각 원소가 자신을 제외한 나머지들의 곱셈이 되는 함수를 작성하라.
단, 나눗셈을 사용하지 않으면서, time complexity O(n) 내에 해결하라.

ex) [1, 2, 3, 4] -> [24, 12, 8, 6]
```
# Solution
자신을 제외하고 좌->우, 우->좌로 누적값을 곱해주면 된다.

|1|2|3|4|
|-:|-:|-:|-:|
|1|1x1|1x1x2|1x1x2x3|
|2x3x4x1|3x4x1|4x1|1|

```java
int[] multiplyAllExceptMe(int[] arr) {
  final int LENGTH = arr.length;
  int[] result = new int[LENGTH];
  
  int leftAcc = 1;
  for(int i = 0; i < LENGTH; ++i) {
    result[i] = leftAcc;
    leftAcc *= arr[i];
  }
  
  int rightAcc = 1;
  for(int j = LENGTH - 1; j >= 0; --j) {
    result[j] *= rightAcc;
    rightAcc *= arr[j];
  }
  
  return result;
}
```
Time complexity: O(n)<br/>
Space complexity: O(n)
