# Problem
https://leetcode.com/problems/binary-tree-preorder-traversal/description/

```
Given a binary tree, return the preorder traversal of its nodes' values.
```

# Solution 1
- Recursive way
```java
public List<Integer> preorderTraversal(TreeNode root) {
  List<Integer> preordered = new ArrayList<>();
  preorder(root, preordered);
  return preordered;
}
private void preorder(TreeNode node, List<Integer> preordered) {
  if(node == null) {
    return ;
  }
  preordered.add(node.val);
  preorder(node.left, preordered);
  preorder(node.right, preordered);
}
```
- Time complexity: O(N)
- Space complexity: O(N)

# Solution 2
- Iterative way using stack
```java
public List<Integer> preorderTraversal(TreeNode root) {
  List<Integer> preorder = new ArrayList<>();
  if(root == null) {
    return preorder;
  }

  Stack<TreeNode> stack = new Stack<>();
  TreeNode cur = root;
  stack.push(cur);
  while(!stack.isEmpty()) {
    TreeNode r = stack.pop();
    preorder.add(r.val);
    if(r.right != null) {
      stack.push(r.right);    
    }
    if(r.left != null) {
      stack.push(r.left);    
    }                
  }
  return preorder;
}
```
- Time complexity: O(N)
- Space complexity: O(N)
