# Problem
```
링크 리스트(linked list)의 머리 노드(head node)와 정수 N이 주어지면, 끝에서 N번째 노드(node)를 제거하고 머리 노드(head node)를 리턴하시오.
단, 리스트를 한번만 돌면서 풀어야합니다. N은 리스트 길이보다 크지 않습니다.
```

예제)<br/>
Input: 1->2->3->4->5, N=2<br/>
Output: 1->2->3->5<br/><br/>

Input: 1->2->3, N=3<br/>
Output: 2->3<br/><br/>

Input: 1, N=1<br/>
Output: null<br/><br/>
 
# Solution
뒤에서 N번째 노드를 제거하기 위해서는 뒤에서 N-1번째 노드를 뒤에서 N+1 번째 노드에 연결 시켜야 한다.<br/>
관건은 리스트를 한번 돌면서 뒤에서 N-1번째 노드를 찾는 것인데 이는 slow pointer, fast pointer를 두어 해결할 수 있다.<br/>
slow pointer는 head를 가리키고, fast pointer는 slow pointer보다 N 개 앞선 노드를 가리키고 있어야 한다.<br/>
fast pointer가 마지막 노드에 도달했을 때, slow pointer는 뒤에서 N-1번째 노드를 가리키고 있다.<br/>
N은 리스트 길이보다 크지 않다고 했으므로 head가 삭제되는 일은 없다는 의미이다.

## Java
```java
Node removeNthNodeFromEnd(Node head, final int N) {
  if(head == null) {
    return null;
  }
  Node slow = head;
  Node fast = head;
  // make fast pointer
  for(int i = 0; i < N; ++i) {
    fast = fast.next;
  }
  // find last (n-1)th node
  while(fast.next != null) {
    slow = slow.next;
    fast = fast.next;
  }
  // delete last nth node
  slow.next = slow.next.next;
  
  return head;
}
```

n이 노드의 전체 갯수일 경우,<br/>
Time complexity: O(n)<br/>
Space complexity: O(1)

<hr/>
## 유사 문제
- [remove nth node from end of list(include head)](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
