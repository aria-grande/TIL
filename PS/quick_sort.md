# Problem
Write a method sorting a given array.
Use quick sort.


# Solution

Quick sort: left, right pointer를 두고 pivot을 정해 pivot보다 작은 값들은 left로, 큰 값들은 right로 분리한다. <br/>
left partition과 right partition에 대해 위의 로직 반복 적용<br/>

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

| 복잡도 | Big-O |
|-----|---------|
| 시간 | avg.: O(nlogn)<br/>worst: O(n^2) |
| 공간 | O(1) |

#### avg time complexity
n의 리스트를 정렬하는데 걸리는 시간을 T(n), c는 임의의 상수라 할 때, 평균 시간 복잡도 계산.
```
T(n) >= cn + 2T(n/2)
     >= cn + 2{c(n/2) + 2T(n/4)}
     >= 2cn + 4T(n/4)
     >= 2cn + 4{c(n/4) + 4T(n/8)}
     >= 6cn + 8T(n/8)
     >= ...
     >= cnlogn + nT(1) = O(nlogn)
```
<hr/>

## 참고 링크
- [퀵 정렬](https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC)
