# Problem
https://leetcode.com/problems/reorder-list/description/
```
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.
```

# Solution1
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
  // time complexity: O(N * N)
  public void reorderList(ListNode head) {
    final int SIZE = getSize(head);
    ListNode node = head;
    for(int i = 0; (i < SIZE / 2) && node != null; ++i) {
      ListNode lastNode = getLastNode(node);
      if(lastNode != null) {
        lastNode.next = node.next;
        node.next = lastNode;
        node = node.next.next;    
      }
    }
  }
  // time complexity: O(N)
  public ListNode getLastNode(ListNode head) {
    ListNode node = head;
    if(node == null) { 
      return null; 
    }
    while(node.next != null) {
      node = node.next;
      if(node.next != null && node.next.next == null) {
        ListNode lastNode = node.next;
        node.next = null;
        return lastNode;
      }
    }
    return null;
  }

  // time complexity: O(N)
  public int getSize(ListNode head) {
    int size = 0;
    ListNode node = head;
    while(node != null) {
      size++;
      node = node.next;
    }
    return size;
  }
}
```

Time complexity: O(N^2)

Space complexity: O(1)

# Solution2(Better)
풀면서: linked list를 reverse 시키는데 꽤나 바보같이 짜고 디버깅했다(ㅠㅠ)
```java
class Solution {
  public void reorderList(ListNode head) {
    if(head == null) {
      return ;
    }
    // 1. find the middle point - time: O(N)
    ListNode p1 = head;
    ListNode p2 = head.next;
    while(p2 != null && p2.next != null) {
      p1 = p1.next;
      p2 = p2.next.next;
    }
    p2 = p1.next;
    // 2. cut the list
    p1.next = null;
    // 3. reverse the last list - time: O(N)
    ListNode reversedP2 = reverse(p2);
    // 4. merge - time: O(N)
    merge(head, reversedP2);
  }

  private ListNode reverse(ListNode head) {
    if(head == null || head.next == null) {
      return head;
    }
    ListNode newHead = head;
    ListNode nextNode = head.next;
    ListNode cur = head.next;
    newHead.next = null;
    while(cur != null) {
      nextNode = cur.next;
      cur.next = newHead;
      newHead = cur;
      cur = nextNode;
    }
    return newHead;
  }

  private void merge(ListNode head1, ListNode head2) {
    ListNode node1 = head1;
    ListNode node2 = head2;
    ListNode nextNode1 = null;
    ListNode nextNode2 = null;
    while(node1 != null && node2 != null) {
      nextNode1 = node1.next;
      nextNode2 = node2.next;
      node2.next = node1.next;
      node1.next = node2;

      node1 = nextNode1;
      node2 = nextNode2;
    }
  }
}
```

Time complexity: O(N)

Space complexity: O(1)
