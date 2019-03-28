# PROBLEM
https://leetcode.com/problems/minimum-depth-of-binary-tree/description/

# SOLUTION
```java
public int minDepth(TreeNode root) {
    if(root == null) {
        return 0;
    }
    int right =  minDepth(root.right) + 1;
        
    int left = minDepth(root.left) + 1;
        
    if(root.left == null) {
        return right;
    }
    if(root.right == null) {
        return left;
    }
    return Math.min(left, right);
}
```

TIME COMPLEXITY: O(N)

SPACE COMPLEXITY: O(1)
