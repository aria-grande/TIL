# Problem
https://leetcode.com/problems/populating-next-right-pointers-in-each-node/

Given a binary tree
```
struct TreeLinkNode {
  TreeLinkNode *left;
  TreeLinkNode *right;
  TreeLinkNode *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

Note:

- You may only use constant extra space.
- Recursive approach is fine, implicit stack space does not count as extra space for this problem.
- You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).

# Solution
왜 medium이지? 노드의 입장에서 children nodes를 케어하면 쉽게 풀리는 문제.

```java
public class Solution {
    public void connect(TreeLinkNode root) {
        if(root == null) {
            return;
        }
        if(root.left != null) {
            root.left.next = root.right;    
        }
        if(root.right != null && root.next != null) {
            root.right.next = root.next.left;
        }
        connect(root.left);
        connect(root.right);
    }
}
```

## Submission Result
- Runtime: 0ms

N이 노드의 갯수라 할 때,

Time complexity: O(N)

Space complexity: O(1) (O(log N) when considers call stack)
