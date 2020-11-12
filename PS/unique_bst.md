# Problem
https://leetcode.com/problems/unique-binary-search-trees/


# Solution

```java
public int numTrees(int n) {
    if (n < 2) {
        return n;
    }
    int[] nums = new int[n + 1];
    nums[0] = 1;
    nums[1] = 1;
    nums[2] = 2;

    for(int i = 3; i <= n; ++i) {
        int num = 0;
        for(int k = 0; k < i; ++k) {
            num += nums[k]*nums[i - 1 - k];
        }

        nums[i] = num;
    }

    return nums[n];
}
```

Time complexity: O(N)

Space complexity: O(N)


# Following Problem
https://leetcode.com/problems/unique-binary-search-trees-ii/

Now, return all BST

# Solution

```java
public List<TreeNode> generateTrees(int n) {
    if (n < 1) {
        return new ArrayList<TreeNode>();
    }
    return generate(1, n);
}

private List<TreeNode> generate(int start, int end) {
    List<TreeNode> result = new ArrayList<>();
    if (start > end) {
        result.add(null);
        return result;
    }
    if (start == end) {
        result.add(new TreeNode(start));
        return result;
    }
    for (int i = start; i <= end; ++i) {
        List<TreeNode> leftLists = generate(start, i - 1);
        List<TreeNode> rightLists = generate(i + 1, end);
        for (TreeNode left : leftLists) {
            for (TreeNode right : rightLists) {
                TreeNode node = new TreeNode(i);
                node.left = left;
                node.right = right;
                result.add(node);
            }
        }
    }

    return result;
}
```

It's called Catalan number: https://en.wikipedia.org/wiki/Catalan_number

Time complexity: O()

Space complexity: O()
