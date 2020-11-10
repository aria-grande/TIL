# Problem
https://leetcode.com/problems/binary-tree-right-side-view/

# Solution

```java
class NullTreeNode extends TreeNode {
    boolean isNull = true;
}
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> rightNums = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        NullTreeNode nullTreeNode = new NullTreeNode();
        queue.add(root);
        queue.add(nullTreeNode);
        while (queue.peek() != null) {
            TreeNode node = queue.poll();

            if (node.left != null) {
                queue.add(node.left);
            }
            if (node.right != null) {
                queue.add(node.right);
            }
            if (queue.peek() != null && queue.peek() == nullTreeNode) {
                queue.poll();
                queue.add(nullTreeNode);
                rightNums.add(node.val);
            }
        }
        return rightNums;
    }
}

```

Time complexity: O(N) when N is the number of the nodes in the tree

Space complexity: O(N)
