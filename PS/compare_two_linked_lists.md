# Problem
https://www.hackerrank.com/challenges/compare-two-linked-lists/problem
```
두 개의 singly linked list가 주어질 때, 두 list가 같은지 판단하는 메소드를 작성하라.
'같다'는 것은 리스트의 길이 및 모든 데이터가 동일함을 의미한다.
```

# Solution

```java
boolean compareLists(SinglyLinkedListNode head1, SinglyLinkedListNode head2) {
    SinglyLinkedListNode node1 = head1;
    SinglyLinkedListNode node2 = head2;
    while(node1 != null && node2 != null) {
        if (node1.data != node2.data) {
            return false;
        }
        node1 = node1.next;
        node2 = node2.next;         
    }
    return node1 == null && node2 == null;
}
```

Time complexity: O(N)<br/>
Space complexity: O(1)
