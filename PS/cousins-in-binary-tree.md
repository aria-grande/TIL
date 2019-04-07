# PROBLEM
https://leetcode.com/problems/cousins-in-binary-tree/

In a binary tree, the root node is at depth 0, and children of each depth k node are at depth k+1.

Two nodes of a binary tree are cousins if they have the same depth, but have different parents.

We are given the root of a binary tree with unique values, and the values x and y of two different nodes in the tree.

Return true if and only if the nodes corresponding to the values x and y are cousins.

# SOLUTION
```java
class Solution {
    class NodeInfo {
        TreeNode parent;
        int depth;
        boolean notFound;
        
        public NodeInfo(TreeNode parent, int depth, boolean notFound){
            this.parent = parent;
            this.depth = depth;
            this.notFound = notFound;
        }
    }
    public boolean isCousins(TreeNode root, int x, int y) {
        NodeInfo ix = findParent(root, x, 0);
        NodeInfo iy = findParent(root, y, 0);
        if(ix.notFound || iy.notFound) {
            return false;
        }
        return ix.parent != iy.parent && ix.depth == iy.depth;
    }
    
    private NodeInfo findParent(TreeNode node, int val, int depth) {
        if(node == null) {
            return new NodeInfo(node, depth, true);
        }
        if((node.left != null && node.left.val == val) || (node.right != null && node.right.val == val)){
            return new NodeInfo(node, depth, false);
        }
        NodeInfo l = findParent(node.left, val, depth + 1);
        NodeInfo r = findParent(node.right, val, depth + 1);
        return l.notFound ? r : l;
    }
}
```

## RESULT
Runtime: 1 ms, faster than 95.05% of Java online submissions for Cousins in Binary Tree.

Memory Usage: 36.7 MB, less than 95.48% of Java online submissions for Cousins in Binary Tree.
