# Problem
https://leetcode.com/problems/closest-binary-search-tree-value/

# Solution

```java
public int closestValue(TreeNode root, double target) {
    int left = Integer.MIN_VALUE;
    int right = Integer.MAX_VALUE;

    TreeNode node = root;
    while(node != null) {
        if(node.val > target) {
            right = Math.min(node.val, right);
            node = node.left;
        }
        else {
            left = Math.max(node.val, left);
            node = node.right;
        }
    }
    if(left == Integer.MIN_VALUE) {
        return right;
    }
    if(right == Integer.MAX_VALUE) {
        return left;
    }
    return (target - left) > (right - target) ? right : left;
}
```
노드의 갯수가 N개라고 할 때,

Time complexity: O(log N)

Space complexity: O(1)

Runtime: almos 0 ms
