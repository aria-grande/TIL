# Problem
https://leetcode.com/problems/univalued-binary-tree/

```
A binary tree is univalued if every node in the tree has the same value.

Return true if and only if the given tree is univalued.
```

# Solution
```java
public boolean isUnivalTree(TreeNode root) {
    if (root == null) {
        return true;
    }
    return isUnivalTree(root.left, root.val) && isUnivalTree(root.right, root.val);
}

private boolean isUnivalTree(TreeNode node, int val) {
    if (node == null) {
        return true;
    }
    if (nodeVal != val) {
        return false;
    }
    return isUnivalTree(node.left, node.val) && isUnivalTree(node.right, node.val);
}
```

Time complexity: O(N), when N is the number of nodes in the tree
Space complexity: O(N)
