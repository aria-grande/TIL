# Problem
https://www.hackerrank.com/challenges/find-the-merge-point-of-two-joined-linked-lists/problem
```
주어진 두 링크드 리스트는 합쳐질 것인데, 합쳐지는 노드를 찾아라. 
찾았다면 그 노드의 data를, 찾지 못했다면 -1을 리턴하는 메소드를 작성하라.
두 리스트의 헤드 노드는 null도 아니고, 같지도 않음을 보장한다.
```

# Solution
두 링크드 리스트가 합쳐진다는 것은 단순히 node.data만 같음을 의미하는 것이 아니다. node의 reference가 같음을 의미하는 것이다.<br/>
1) 문제를 해결하기 위해서는 각 리스트의 길이를 알아야 하고,
2) 길이가 긴 링크드 리스트의 포인터를 difference만큼 움직인 후, 
3) 두 리스트의 포인터를 같이 움직이며 비교해야 한다.

문제에 따르면, 두 리스트의 헤드 노드는 null도 아니고 같지도 않으므로 mergedNode는 절대 head가 될 수 없다. <br/>
따라서, 두 리스트의 길이가 같다면, 포인터를 한 번씩 move 한 후 비교해야 한다.<br/>

```java
int getLength(SignlyLinkedListNode node) {
  int len = 0;
  while(node != null) {
    node = node.next;
    len++;
  }
  return len;
}

SinglyLinkedListNode moveForward(SinglyLinkedListNode node, int n) {
  while(n-- > 0) {
    node = node.next;
  }
  return node;
}

int findMergedNode(SinglyLinkedListNode head1, SinglyLinkedListNode head2) {
  final int len1 = getLength(head1);
  final int len2 = getLength(head2);
  SinglyLinkedListNode node1 = head1;
  SinglyLinkedListNode node2 = head2;
  if(len1 == len2) {
    node1 = moveForward(node1, 1);
    node2 = moveForward(node2, 1);
  }
  else if (len1 < len2) {
    node2 = moveForward(node2, len2 - len1);
  }
  else {
    node1 = moveForward(node1, len1 - len2);
  }
  
  while(node1 != null && node2 != null) {
    if (node1 == node2) {
      return node1.data;
    }
    node1 = node1.next;
    node2 = node2.next;
  }
  return -1;
}
```
두 링크드 리스트의 길이를 각 N, M이라 할 때,<br/>
Time complexity: O(N+M)<br/>
Space complexity: O(1)
