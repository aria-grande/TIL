# PROBLEM
https://leetcode.com/problems/invert-binary-tree/

# SOLUTION

class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null) {
            return null;
        }
        TreeNode tmp = invertTree(root.left);
        root.left = invertTree(root.right);
        root.right = tmp;
        return root;
    }
}

Time complexity: O(N)

Space compexity: O(N)

Runtime: 0ms(leetcode)
