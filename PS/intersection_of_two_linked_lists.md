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

# Solution2(Better Code)
list1의 길이가 n이고 list2의 길이가 m이라 할 때, intersection 노드 부터 맨 끝까지는 (n-m) 혹은 (m-n)이다.

편의상 list1이 더 길다고 해보자. 그럼 intersectinon 노드(IN)부터 맨 끝까지의 길이는 (n-m)이고,

list1에서 IN까지의 길이는 `(n - (n - m)) = m`이다.

list2에서 IN까지의 길이는 `(m - (n - m)) = 2*m - n`이다.

리스트를 순회하는 포인터가 두 개 있다고 할 때, 두 포인터가 만나려면 위의 두 값을 갖게 만족시킬만큼 돌아야 한다.

list1에서 IN까지 돌고 list2의 길이만큼 더 돌고, list2에서 IN까지 돌고 list1의 길이만큼 더 돌면 서로 만나지 않을까?

`(m + m) = (2*m - n + n)`



```java
```
