# Problem
https://leetcode.com/problems/reorder-list/description/
```
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.
```

# Solution
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
