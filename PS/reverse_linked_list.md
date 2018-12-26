# Problem
https://leetcode.com/problems/reverse-linked-list/description/

# Solution

class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode reversed = null;
        while(head != null) {
            ListNode n = new ListNode(head.val);
            n.next = reversed;
            reversed = n;
            head = head.next;
        }
        return reversed;
    }
}

Time complexity: O(N)

Space complexity: O(N)
