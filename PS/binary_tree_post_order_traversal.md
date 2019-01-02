# Problem
https://leetcode.com/problems/binary-tree-postorder-traversal/

Given a binary tree, return the postorder traversal of its nodes' values.
```
Example:

Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
```
**Follow up: Recursive solution is trivial, could you do it iteratively?**

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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> traversal = new ArrayList<>();
        if(root == null) {
            return traversal;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()) {
            TreeNode top = stack.pop();
            traversal.add(0, top.val);
            if(top.left != null) {
                stack.push(top.left);   
            }
            if(top.right != null) {
                stack.push(top.right);    
            }
        }
        return traversal;
    }
}
```

Time complexity: O(N)

Space complexity: O(N)

---
재귀로 푸는건 쉬운데, iterative 하게 푸는 것도 어렵진 않았다. 왜 난이도가 hard지..뭔갈 놓친걸까?
