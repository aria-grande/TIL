# Problem
Write a function of merge sort.

# Solution

Merge sort: divide & conquer의 대표적인 예시.<br/>
subarray의 length가 2 이하가 될때까지 divide, 두 개 간단히 대소비교 후 sort<br/>
subarray끼리 merge

```java
void sort(int[] arr) {
  mergeSort(arr, 0, arr.length - 1);
}
void mergeSort(int[] arr, int left, int right) {
    if (right - left < 1) {
      return;
    }
    if (right - left == 1) {
      if(arr[right] < arr[left]) {
      	swap(arr, left, right);
      }
      return;
    }
    int mid = (left + right) / 2;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);

    int lp = left;
    int rp = mid + 1;
    int[] merged = new int[right - left + 1];
    for (int p = 0; p < merged.length; ++p) {
      if (lp > mid) {
        merged[p] = arr[rp++];
      }
      else if (rp > right) {
        merged[p] = arr[lp++];
      }
      else if (arr[lp] < arr[rp]) {
        merged[p] = arr[lp++];
      }
      else {
        merged[p] = arr[rp++];
      }
    }
    
    for(int elem : merged) {
      arr[left++] = elem;
    }
  }
```

Time complexity: O(nlogn)<br/>
Space complexity: O(n)

<hr/>

## 참고 링크
- [합병 정렬](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC)
- [Merge sort](https://www.geeksforgeeks.org/merge-sort/)
