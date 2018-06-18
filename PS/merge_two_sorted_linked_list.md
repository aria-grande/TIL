# Problem
https://www.hackerrank.com/challenges/merge-two-sorted-linked-lists/problem
```
두개의 정렬된(sorted) 정수 링크드 리스트(linked list)가 주어지면, 두 리스트를 합친 정렬된 링크드 리스트를 만드시오.

예제)
Input: 1->2->3, 1->2->3
Output: 1->1->2->2->3->3

Input: 1->3->5->6, 2->4
Output: 1->2->3->4->5->6
```

# Solution
```java
List<Integer> mergeAndSort(List<Integer> l1, List<Integer> l2) {
  if (l1.isEmpty()) {
    return l2;
  }
  if (l2.isEmpty()) {
    return l1;
  }
  List<Integer> merged = new ArrayList<Integer>();
  
  int[] arr1 = l1.stream().mapToInt(i -> i).toArray();
  int[] arr2 = l2.stream().mapToInt(i -> i).toArray();
  int p1 = 0, p2 = 0;
  
  while(p1 < arr1.length && p2 < arr2.length) {
    if (arr1[p1] <= arr2[p2]) {
      merged.add(arr1[p1++]);
    }
    else {
      merged.add(arr2[p2++]);
    }
  }
  
  while(p1 < arr1.length) {
    merged.add(arr1[p1++]);
  }
  while(p2 < arr2.length) {
    merged.add(arr2[p2++]);
  }
  
  return merged;
}
```
두 리스트의 사이즈를 각각 N1, N2라고 할 때,<br/>
Time complexity: O(N1+N2)<br/>
Space complexity: O(N1+N2)

