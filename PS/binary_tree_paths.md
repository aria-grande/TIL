# Problem
https://leetcode.com/problems/binary-tree-paths/

# Solution
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> paths = new ArrayList<>();     
        dfs(root, paths, "");
        return paths;
    }
    
    private void dfs(TreeNode node, List<String> paths, String parent) {
        if(node == null) {
            return;
        }
        parent += ("->" + node.val);
        if(node.left == null && node.right == null) {
            paths.add(parent.substring(2));
        }
        else {
            dfs(node.left, paths, parent);
            dfs(node.right, paths, parent);
        }
    }
}
```

Suppose N is the number of nodes in the given tree,

Time complexity: O(N)

Space complexity: O(N) considered call stack
