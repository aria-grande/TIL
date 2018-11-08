# Problem
https://leetcode.com/problems/maximum-binary-tree/description/
```
Given an integer array with no duplicates. 
A maximum tree building on this array is defined as follow:

1. The root is the maximum number in the array.
2. The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.
3. The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.

Construct the maximum tree by the given array and output the root node of this tree.
```

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
  public TreeNode constructMaximumBinaryTree(int[] nums) {
    return construct(nums, 0, nums.length - 1);
  }

  private TreeNode construct(int[] nums, int sp, int ep) {
    if(sp >= nums.length || ep >= nums.length || sp > ep) {
      return null;
    }
    int max = 0;
    int idx = sp;
    for(int i = sp; i <= ep; ++i) {
      if(nums[i] > max) {
        max = nums[i];
        idx = i;
      }
    }

    TreeNode root = new TreeNode(max);
    root.left = construct(nums, sp, idx - 1);
    root.right = construct(nums, idx + 1, ep);

    return root;
  }
}
```

Time complexity: O(N^2)

Space complexity: O(1) (재귀 스택까지 포함한다면 O(N))
