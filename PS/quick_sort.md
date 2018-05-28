# Problem
Write a method sorting a given array.
Use quick sort.


# Solution

Quick sort: left, right pointer를 두고 pivot을 정해 pivot보다 작은 값들은 left로, 큰 값들은 right로 분리한다. 
left partition과 right partition에 대해 위의 로직 반복 적용

```java
void sort(int[] arr) {
  quickSort(arr, 0, arr.length - 1);
}

void quickSort(int[] arr, int left, int right) {
  if (arr == null || arr.length == 0 || left >= right) {
    return ;
  }
  int partitionedIdx = partition(arr, left, right);
  quickSort(arr, left, partitionedIdx - 1);
  quickSort(arr, partitionedIdx + 1, right);
}

int partition(int[] arr, int left, int right) {
  int pivot = arr[(left + right) / 2];
  while(left < right) {
    while(arr[left] < pivot && left < right) {
      ++left;
    }
    while(pivot < arr[right] && left < right) {
      --right;
    }
    if(left < right) {
      swap(arr, left, right);
    }
  }
  return left;
}

void swap(int[] arr, int idx1, int idx2) {
    int tmp = arr[idx2];
    arr[idx2] = arr[idx1];
    arr[idx1] = tmp;
}
```

| 복잡도 | 평균 | worst |
|------|-----|-------|
| 시간  | O(nlogn) | O(n^2) |
