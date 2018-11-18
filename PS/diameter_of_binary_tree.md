# Problem
https://leetcode.com/problems/diameter-of-binary-tree/
```
Given a binary tree, you need to compute the length of the diameter of the tree. 
The diameter of a binary tree is the length of the longest path between any two nodes in a tree. 
This path may or may not pass through the root.
```

# Solution
- left subtree의 높이와 right subtree의 높이를 각각 L, R이라 할 때, MAX(L) + MAX(R)이 diameter가 된다.

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
    int maxLength;
    public int diameterOfBinaryTree(TreeNode root) {
        maxLength = 1;
        getDepth(root);
        return maxLength - 1;
    }
    
    private int getDepth(TreeNode node) {
        if(node == null) {
            return 0;
        }
        int left = getDepth(node.left);
        int right = getDepth(node.right);
        maxLength = Math.max(maxLength, left + right + 1);
        return Math.max(left, right) + 1;
    }
}
```
노드의 갯수를 N이라 할 때,

Time complexity: O(N)

Space complexity: O(1) (call stack을 고려한다면 O(N))
