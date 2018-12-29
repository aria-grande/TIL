# Problem
https://leetcode.com/problems/binary-search-tree-iterator/
```
Implement an iterator over a binary search tree (BST). 
Your iterator will be initialized with the root node of a BST.

Calling next() will return the next smallest number in the BST.
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
class BSTIterator {

    int current;
    Stack<TreeNode> inorder;
    
    public BSTIterator(TreeNode root) {
        inorder = new Stack<>();
        traverse(root);
    }
    
    private void traverse(TreeNode node) {
        if(node == null) {
            return ;
        }
        if(node.right != null) {
            traverse(node.right);
        }
        inorder.push(node);
        if(node.left != null) {
            traverse(node.left);
        }        
    }
    
    /** @return the next smallest number */
    public int next() {
        return inorder.pop().val;
    }
    
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !inorder.isEmpty();
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```

일단 brute-force 하게 풀어본다.
