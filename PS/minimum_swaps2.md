# Problem
https://www.hackerrank.com/challenges/minimum-swaps-2/problem?h_l=playlist&slugs%5B%5D=interview&slugs%5B%5D=interview-preparation-kit&slugs%5B%5D=arrays
```
For a given unordered array consisting of consecutive integers without any duplications,
you have to sort the array in ascending order using only swapping.
Here, find the minimum number of swapping required to order.

ex)
[4,3,2,1] -> 2 
- (0,3) swap
- (1,2) swap
```

# Solution
연속된 정수이고 중복이 없다고 했으므로, 오름차순 정렬된 배열의 원소는 index + 1과 같아야 한다.
고로, `arr[index] != index + 1` 이라면, 현 위치(`index`)와 제자리(`arr[index]-1`)의 인덱스를 기준으로 제자리를 찾을 때까지 스와핑 해줘야 한다.

```java
int getSwapCount(int[] arr) {
  int count = 0;
  for(int idx = 0; idx < arr.length; ++idx) {
    while(arr[idx] != idx + 1) {
      swap(arr, idx, arr[idx] - 1);
      count++;
    }
  }
  return count;
}

void swap(int[] arr, int p1, int p2) {
  int tmp = arr[p1];
  arr[p1] = arr[p2];
  arr[p2] = tmp;
}
```
arr의 길이가 N이라고 할 때,
Time complexity: O(N)<br/>
Space complexity: O(1)
