# Problem
https://leetcode.com/problems/trim-a-binary-search-tree/
```
Given a binary search tree and the lowest and highest boundaries as L and R, 
trim the tree so that all its elements lies in [L, R] (R >= L).
You might need to change the root of the tree, 
so the result should return the new root of the trimmed binary search tree.
```

# Solution

```java
public TreeNode trimBST(TreeNode root, int L, int R) {
    return trim(root, L, R);
}

private TreeNode trim(TreeNode node, int L, int R) {
    if(node == null) {
        return null;
    }
    if(node.val < L) {
        return trim(node.right, L, R);
    }
    if(node.val > R) {
        return trim(node.left, L, R);
    }
    node.left = trim(node.left, L, R);
    node.right = trim(node.right, L, R);
    return node;
}
````

Time complexity: O(N)

Space complexity: O(1) (O(N) when considered call stack)
