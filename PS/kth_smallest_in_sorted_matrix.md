# Problem
https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/
```
Given a n x n matrix where each of the rows and columns are sorted in ascending order, 
find the kth smallest element in the matrix.
Note that it is the kth smallest element in the sorted order, not the kth distinct element.
```

# Solution
- 여분의 자료구조를 사용하지 않고 풀어보려 했으나 실패 ㅠㅠ
- [TreeMap](https://docs.oracle.com/javase/8/docs/api/index.html?java/util/TreeMap.html)을 사용하면 쉽게 해결 가능! 
  > SortedMap의 구현체로 key에 대해 ordering을 한 map이다. 이에 따른 insertion 시간 복잡도는 N개의 element를 넣을 경우 O(N*log(N))이다.
  
```java
  public int kthSmallest(int[][] matrix, int k) {
    Map<Integer, Integer> counts = new TreeMap<Integer, Integer>();
    for(int[] row : matrix) {
      for(int e : row) {
        counts.put(e, counts.getOrDefault(e, 0) + 1);
      }
    }
    for(int num : counts.keySet()) {
      int count = counts.get(num);
      k -= count;
      if(k <= 0) {
        return num;
      }
    }
    return -1;
  }
```
