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


# Solution w/o global variable
2019.01.19

```java
class Solution {
    public TreeNode convertBST(TreeNode node) {
        convert(node, 0);
        return node;
    }
    
    private int convert(TreeNode node, int acc) {
        if(node == null) {
            return acc;
        }
        int right = (node.right == null) ? acc : convert(node.right, acc);
        node.val += right;
        return convert(node.left, node.val);
    }
}
```
노드의 갯수가 N 개라 할 때,
Time complexity: O(N)

Space complexity: O(log N) (O(N) when the worst case)
