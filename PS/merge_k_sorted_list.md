# Problem
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
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
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode result = new ListNode(0);
        ListNode rn = result;
        boolean listIsEnd = false;
        while(!listIsEnd) {
            listIsEnd = true;
            int min = Integer.MAX_VALUE;
            for(ListNode n : lists) {
                if(n != null) {
                    min = Math.min(min, n.val);
                    listIsEnd = false;
                }
            }
            for(int i = 0; i < lists.length; ++i) {
                ListNode n = lists[i];
                if(n != null && n.val == min) {
                    rn.next = new ListNode(min);
                    rn = rn.next;
                    lists[i] = n.next;
                }
            }
        }
        return result.next;
    }
}
```
Suppose that k lists, and the length of the list is N.

Time complexity: O(kN)

Space complexity: O(kN)

Runtime: 11ms
