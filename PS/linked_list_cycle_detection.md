# Problem
https://www.hackerrank.com/challenges/detect-whether-a-linked-list-contains-a-cycle/problem
```
For a given linked list, determine if there's a cycle 
that any node is visited more than once while traversing a list.
```

# Solution
고전적인 토끼와 거북이 문제이다.

움직일 때, 한 노드씩만 이동하는 slow pointer, 두 녿씩 이동하는 fast pointer를 두고 계속 달리다 보면,<br/>
cycle이 존재할 경우 언젠가 두 포인터가 만난다.

```java
boolean hasCycle(Node head) {
  Node slow = head;
  Node fast = head;
  while(fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
    if(slow == fast) {
      return true;
    }
  }
  return false;
}
```

Time complexity: O(N)<br/>
Space complexity: O(1)
