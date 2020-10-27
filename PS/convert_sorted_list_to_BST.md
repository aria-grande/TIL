# Problem
https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/
```
Given the head of a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
```

# Solution
```java
 public TreeNode sortedListToBST(ListNode head) {
    int length = 0;
    ListNode node = head;
    while (node != null) {
        length++;
        node = node.next;
    }

    return convert(head, length);
}

private TreeNode convert(ListNode head, final int length) {
    if (head == null || length <= 0) {
        return null;
    }
    final int mid = length / 2;
    ListNode node = head;
    for (int i = 0; i < mid; ++i) {
        node = node.next;
    }
    if (node == null) {
        return null;
    }
    TreeNode root = new TreeNode(node.val);
    root.left = convert(head, mid);
    root.right = convert(node.next, length - mid - 1);

    return root;
}
```

Since it's sorted, mid Node will be the root node.

Time complexity: O(N), when N is the size of sorted list

Space complexity: O(log N)
