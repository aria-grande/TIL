# Problem
https://www.glassdoor.com/Interview/Given-an-array-of-integers-where-each-element-points-to-the-index-of-the-next-element-how-would-you-detect-if-there-is-a-cy-QTN_69928.htm
```
Given an array of integers where each element points to the index of the next element,
how would you detect if there is a cycle in this array?
```
# Solution
현재 방문 중인 index가 방문 한 적이 없다면 방문 했다는 의미로 값을 -1로 바꿔주고, 방문한 적이 있다면 cycle이므로 true를 리턴한다.


```java
boolean hasCycle(int[] arr) {
  final int COUNT = arr.length;
  int curIdx = 0;
  
  while(COUNT-- > 0) {
    if(arr[curIdx] == -1) {
      return true;
    }
    
    int oldIdx = curIdx;
    curIdx = arr[curIdx];
    arr[oldIdx] = -1;
  }
  
  return false;
}
```
N이 array의 length라 할 때,<br/>
Time complexity: O(N)<br/>
Space complexity: O(1)
