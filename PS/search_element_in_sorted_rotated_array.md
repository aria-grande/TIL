# Problem
https://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/
```
정렬된 정수 배열이 있습니다. 이 배열의 모든 원소들을 오른쪽으로 랜덤하게 Z번 이동하였습니다.
예를 들면 [1, 2, 3, 4, 5] -> [3, 4, 5, 1, 2].

이런 배열과 정수 K 가 주어지면, 배열안에 K가 존재하는지 찾으시오.
존재한다면 배열의 인덱스, 존재하지 않다면 -1 을 리턴하시오.
시간복잡도 제한 O(log N).
```

# Solution
```java
int find(int[] arr, final int K, int left, int right) {
  int mid = (left + right) / 2;
  int[] answer = {left, mid, right};
  for(int e : answer) {
    if(arr[e] == K) {
      return e;
    }
  }

  boolean kIsInLeft = arr[left] < K && K < arr[mid];
  boolean kIsInRight = arr[mid] < K && K < arr[right];
  if(kIsInLeft || (arr[mid] < arr[right] && !kIsInRight)) {
    return find(arr, K, left + 1, mid - 1);
  }
  if(kIsInRight || (arr[left] < arr[mid] && !kIsInLeft)) {
    return find(arr, K, mid + 1, right - 1);
  }

  return -1;
}
```

Time complexity: O(log N)

Space complexity: O(1)<br/>
재귀 스택을 포함한다면 O(log N)
