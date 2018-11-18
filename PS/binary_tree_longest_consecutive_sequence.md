# Problem
https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/
```
Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. 
The longest consecutive path need to be from parent to child (cannot be the reverse).
```

# Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
  public int longestConsecutive(TreeNode root) {
    return root == null ? 0 : getLength(root, 1);
  }

  private int getLength(TreeNode node, int len) {
    if(node == null) {
        return len;
    }
    int max = len;
    if(node.left != null) {
      int newLen = (node.left.val == node.val + 1) ? len + 1 : 1;
      max = Math.max(max, getLength(node.left, newLen));
    }
    if(node.right != null) {
      int newLen = (node.right.val == node.val + 1) ? len + 1 : 1;
      max = Math.max(max, getLength(node.right, newLen));
    }
    return max;
  }
}
```
노드의 갯수가 N 개라 할 때,

Time complexity: O(N)

Space complexity: O(1) (O(N) when considered stack call)
