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
