# Problem
https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/
```
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree 
in which the depth of the two subtrees of every node never differ by more than 1.
```

# Solution

```java
public TreeNode sortedArrayToBST(int[] nums) {
    return convert(nums, 0, nums.length - 1);
}

private TreeNode convert(int[] nums, int sp, int ep) {
    if(sp > ep) {
        return null;
    }
    int mid = (sp + ep) / 2;
    TreeNode node = new TreeNode(nums[mid]);
    node.left = convert(nums, sp, mid - 1);
    node.right = convert(nums, mid + 1, ep);
    return node;
}
```

Time complexity: O(N)

Space complexity: O(N)
