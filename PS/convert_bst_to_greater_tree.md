# Problem
https://leetcode.com/problems/convert-bst-to-greater-tree/


Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.


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
    private int acc = 0;
    
    public TreeNode convertBST(TreeNode node) {
        if(node != null) {
            convertBST(node.right);
            acc += node.val;
            node.val = acc;
            convertBST(node.left);
        }
        return node;
    }
}
```

Time complexity:O(N)

Space complexity: O(N)
