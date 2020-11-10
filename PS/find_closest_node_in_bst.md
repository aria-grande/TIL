# Problem
Given a binary search tree, find node in the tree that is closest to a given number.
Suppose that given number is always in the tree.

# Solution
```java
/**
class TreeNode {
  int val;
  TreeNode left;
  TreeNode right;
}
**/
TreeNode getClosest(TreeNode root, int num) {
  if (root == null) {
    return null;
  }
  TreeNode parent = findParentOfNum(root, num, root);
  if (parent == null) {
    return null;
  }

  int diff1 = Math.abs(parent.val - num);
  int diff2 = Integer.MAX_VALUE;
  int diff3 = Integer.MAX_VALUE;

  TreeNode node = (parent.left != null && parent.left.val == num) ? parent.left : parent.right;
  if (root.val == num) {
    node = root;
    diff1 = Integer.MAX_VALUE;
  }
  if (node.left != null) {
    diff2 = Math.abs(node.left.val - num);
  }
  if (node.right != null) {
    diff3 = Math.abs(node.right.val - num);
  }
  int minDiff = Math.min(Math.min(diff1, diff2), diff3);
  if (minDiff == diff1) {
    return parent;
  }
  if (minDiff == diff2) {
    return node.left;
  }
  return node.right;
}

private TreeNode findParentOfNum(TreeNode node, int num, TreeNode parent) {
  if (node == null) {
    return null;
  }
  if (node.val == num) {
    return parent;
  }
  if (node.val < num) {
    return findParentOfNum(node.right, num, node);
  }
  return findParentOfNum(node.left, num, node);
}
```

When the number of nodes in the tree is N,

Time complexity: O(log N) (in the worst case, O(N))

Space complexity: O(log N) (in the worst case, O(N))


# Following problem - 1
Let's suppose that it's not guaranteed that the given target number is in the BST

```java
static TreeNode getClosest(TreeNode root, int target) {
    if (root == null) {
        return null;

    }
    int diff = Math.abs(root.val - target);
    if (diff == 0) {
        return root;
    }

    TreeNode nodeToSearch = (root.val < target) ? root.right : root.left;
    TreeNode subClosest = getClosest(nodeToSearch, target);
    if (subClosest == null) {
        return root;
    }
    int diff2 = Math.abs(subClosest.val - target);
    if (diff < diff2) {
        return root;
    }
    return subClosest;
}
```

Time complexity: O(log N) (in the worst case, O(N))

Space complexity: O(log N) (in the worst case, O(N))
