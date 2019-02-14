# Problem
Write a program to find the node at which the intersection of two singly linked lists begins.

https://leetcode.com/problems/intersection-of-two-linked-lists/description/

# Solution

```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    ListNode n1 = headA;
    ListNode n2 = headB;
    while(n1 != null && n2 != null) {
        if(n1 == n2) {
            return n1;
        }
        n1 = n1.next;
        n2 = n2.next;
    }
    ListNode longer;
    ListNode shorter;
    ListNode n;
    if(n1 != null) { // n1 is longer
        longer = headA;
        shorter = headB;
        n = n1;
    }
    else if(n2 != null) {   // n2 is longer
        longer = headB;
        shorter = headA;
        n = n2;
    }
    else {
        return null;
    }

    while(n != null) {
        n = n.next;
        longer = longer.next;
    }
    while(longer != null && shorter != null) {
        if(longer == shorter) {
            return longer;
        }
        longer = longer.next;
        shorter = shorter.next;
    }
    return null;
}
```
Suppose the length of one list is N, and the other is M.

Time complexity: O(N + M)

Space complexity: O(1)
