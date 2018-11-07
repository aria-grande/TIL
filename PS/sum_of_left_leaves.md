# Problem
https://leetcode.com/problems/sum-of-left-leaves/description/
```
Find the sum of all left leaves in a given binary tree.
```

# Solution

[3]인 경우 3은 left leaf node가 아니므로 리턴 값은 0이어야 한다.

```java
class Solution {
  public int sumOfLeftLeaves(TreeNode root) {
    return sum(root, false);
  }

  private int sum(TreeNode node, boolean left) {
    if(node == null) {
      return 0;
    }
    if(node.left == null && node.right == null) {   // leaf node
      return left ? node.val : 0;
    }
    return sum(node.left, true) + sum(node.right, false);
  }
}
```

Tree의 총 노드 갯수를 N이라 할 때,

Time complexity: O(N)

Space complexity: O(1) (O(N) if considers call stack)
