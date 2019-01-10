# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/93/linked-list/772
```
Given a singly linked list, determine if it is a palindrome.
```

# Solution

```java
boolean isPalindrome(ListNode head) {
    if(head == null) {
        return true;
    }
    final int size = getSize(head);
    Stack<Integer> half = new Stack<Integer>();
    ListNode node = head;
    for(int i = 0; i < size / 2; ++i) {
        half.push(node.val);
        node = node.next;
    }
    if(size % 2 == 1) {
        node = node.next;
    }
    while(node != null) {
        if(node.val != half.pop()) {
            return false;
        }
        node = node.next;
    }
    return true;
}

int getSize(ListNode head) {
  int size = 0;
  ListNode n = head;
  while(n != null) {
      n = n.next;
      size++;
  }
  return size;
}
```
Time complexity: O(N)<br/>
Space complxity: O(N)

# Solution 2(Better)

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
    public boolean isPalindrome(ListNode head) {
        int len = 0;
        ListNode node = head;
        while(node != null) {
            len++;
            node = node.next;
        }
        final int half = len / 2;
        
        StringBuilder front = new StringBuilder();
        StringBuilder back = new StringBuilder();
        ListNode move = head;
        int i = 0;
        for(; i < half; ++i) {
            front.append(move.val);
            move = move.next;
        }
        if(len % 2 == 1) {
            move = move.next;
            i++;
        }
        for(; i < len; ++i) {
            back.insert(0, move.val);
            move = move.next;    
        }
        return front.toString().equals(back.toString());
    }
}
```

Time complexity: O(N)

Space complexity: O(1)
