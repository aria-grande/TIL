# Problem
https://leetcode.com/problems/odd-even-linked-list/
```
Given a singly linked list, group all odd nodes together followed by the even nodes. 
Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.
```

# Solution1
Solved using in-place
```java
public ListNode oddEvenList(ListNode head) {
    if(head == null || head.next == null) {
        return head;
    }
    ListNode p1 = head;
    ListNode p2 = head.next.next;

    int count = 2;
    while(p2 != null) {
        ListNode next = p1.next;
        ListNode n = p1;
        for(int j = count - 1; j > 0; --j) {
            n = n.next;
        }
        n.next = p2.next;
        p1.next = p2;
        p2.next = next;

        count++;
        for(int i = count; i > 0 && p2 != null; --i) {
            p2 = p2.next;
        }
        p1 = p1.next;
    }
    return head;
}
```
Time: 31ms

Time complexity:(N^2)

Space complexity: O(1)

# Solution 2
odd와 even headers를 별도로 선언하는 것은 O(1)이므로 가능하다.

```java
public ListNode oddEvenList(ListNode head) {
    if(head == null || head.next == null) {
        return head;
    }
    ListNode odd = head;
    ListNode even = head.next;
    ListNode evenHead = even;
    while(even != null && even.next != null) {
        odd.next = even.next;
        odd = odd.next;
        even.next = odd.next;
        even = even.next;
    }
    odd.next = evenHead;
    return head;
}
```
Time: 2ms

Time complexity: O(N)

Space complexity: O(1)
