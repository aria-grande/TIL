# PROBLEM
https://leetcode.com/problems/remove-linked-list-elements/

# SOLUTION

public ListNode removeElements(ListNode head, int val) {
        while(head != null && head.val == val){
            head = head.next;
        }
        if(head == null) {
            return head;
        }
        ListNode prev = head;
        ListNode cur = head.next;
        while(cur != null) {
            if(cur.val == val) {
                prev.next = cur.next;
                cur = cur.next;
            }
            else {
                prev = prev.next;
                cur = cur.next;
            } 
        }
        return head;
    }
    
Time complexity: O(N)

Space complexity: O(1)
