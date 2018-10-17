# Problem
```
Given a binary tree, return all duplicate subtrees. 
For each kind of duplicate subtrees, you only need to return the root node of any one of them.

Two trees are duplicate if they have the same structure with same node values.

Example 1:
       1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
The following are two duplicate subtrees:

      2
     /
    4

and

    4
    
Therefore, you need to return above trees' root in the form of a list.
```
https://leetcode.com/problems/find-duplicate-subtrees/

# Solution
어떻게 풀 수 있을까 고민하다보니, tree traverse를 이용해서 string으로 만들고 이를 key값으로, 출현 횟수를 value로 하는 map을 구성하면 좋겠다는 아이디어가 떠올랐다.
후에 출현 횟수가 2 이상인 노드들을 list에 넣어 리턴하면 끝!

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
  public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
    Map<String, Integer> counts = new HashMap<String, Integer>();
    Map<String, TreeNode> nodeMap = new HashMap<String, TreeNode>();

    Stack<TreeNode> stack = new Stack<TreeNode>();
    stack.push(root);

    while(!stack.isEmpty()) {
      TreeNode node = stack.pop();
      if(node != null) {
        String treeStr = toPreorder(node);
        counts.put(treeStr, counts.getOrDefault(treeStr, 0) + 1);
        nodeMap.put(treeStr, node);

        stack.push(node.right);
        stack.push(node.left);
      }
    }

    List<TreeNode> trees = new ArrayList<TreeNode>();
    for(String key : counts.keySet()){
      if (counts.get(key) > 1) {
        trees.add(nodeMap.get(key));
      }
    }
    return trees;
  }

  private String toPreorder(TreeNode root) {
      StringBuilder sb = new StringBuilder();
      Stack<TreeNode> stack = new Stack<TreeNode>();
      stack.push(root);
      while(!stack.isEmpty()) {
        TreeNode node = stack.pop();
        if(node == null) {
          sb.append("# ");
        } else {
          sb.append(node.val + " ");
          stack.push(node.right);
          stack.push(node.left);
        }
      }
      return sb.toString().trim();
  }
}
```

Time complexity: O(N^2)

Space complexity: O(N^2)
