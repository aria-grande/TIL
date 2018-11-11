# Problem
https://leetcode.com/problems/swap-nodes-in-pairs/
```
Given a linked list, swap every two adjacent nodes and return its head.
```

# Solution
- 세 개의 노드 포인터가 필요하다. 한 개는 이전 페어와의 연결고리를 위한 last node of the previous pair, 두 개는 nodes to swap.
- 리턴은 초기 리스트의 두 번째 노드(`head.next`)를 리턴해야 함에 유의하자. 이를 미리 저장해두고 있어야 한다. 리스트가 변형된 이후의 head.next는 원하는 결괏값이 아닐테니까!

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public ListNode swapPairs(ListNode head) {
    if(head == null || head.next == null) {
        return head;
    }
    ListNode result = head.next;

    ListNode p0 = null;
    ListNode p1 = head;
    ListNode p2 = head.next;

    while(p2 != null) {
        p1.next = p2.next;
        p2.next = p1;
        if(p0 != null) {
            p0.next = p2;    
        }
        p0 = p1;
        p1 = p1.next;
        p2 = (p1 == null) ? null : p1.next;
    }
    return result;
}
```

Time complexity: O(N)

Space complexity: O(1)
