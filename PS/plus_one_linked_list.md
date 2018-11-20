# Problem
https://leetcode.com/problems/plus-one-linked-list/

```
Given a non-negative integer represented as non-empty a singly linked list of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.
The digits are stored such that the most significant digit is at the head of the list.
```

# Solution 1

```java
class Solution {
    int leadingNum;
    public ListNode plusOne(ListNode head) {
        if(head == null) {
            return null;    
        }
        leadingNum = 1;
        return plus(head, head);
    }
    
    private ListNode plus(ListNode head, ListNode node) {
        if(node.next == null) {
            int sum = node.val + leadingNum;
            node.val = sum % 10;
            leadingNum = sum / 10;
            if(leadingNum == 1) {
                ListNode newHead = new ListNode(1);
                newHead.next = head;
                return newHead;    
            }
            return node;
        }
        plus(head, node.next);
        
        int newSum = node.val + leadingNum;
        node.val = newSum % 10;
        leadingNum = newSum / 10;
        if(leadingNum == 1) {
            ListNode newHead = new ListNode(1);
            newHead.next = head;
            return newHead;
        }
        return head;
    }
}
```

# Solution 2(Better code)
```java 
class Solution {
    public ListNode plusOne(ListNode head) {
        if(head == null) {
            return null;    
        }
        if(getLeadingNum(head) == 0) {
            return head;
        }
        ListNode newHead = new ListNode(1);
        newHead.next = head;
        return newHead;
    }
    
    private int getLeadingNum(ListNode node) {
        int carry = (node.next == null) ? 1 : getLeadingNum(node.next);
        int sum = node.val + carry;
        node.val = sum % 10;
        return sum / 10;
    }
}
```

Time complexity: O(N)

Space complexity: O(1) (O(N) when considers call stack)
