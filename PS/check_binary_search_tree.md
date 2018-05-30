# Problem
Determine if it is a BST for a given tree.

# Solution

## BST
Binary Search Tree의 약자로 tree 구조이다.<br/>
각 노드는 두 개 이하의 children 노드를 가지고 있으며, 한 노드의 left subtree는 이 노드의 값보다 작고, right subtree는 노드의 값보다 크다.


```java
boolean isBST(Node head) {
  if (head  == null) {
    return true;
  }
  return checkBST(head, Integer.MIN_VALUE, Integer.MAX_VALUE);
}

boolean checkBST(Node node, int min, int max) {
  if (node == null) {
    return true;
  }
  int data = node.data;
  return (min < data && data < max) && 
        checkBST(node.left, min, Math.min(max, data)) && checkBST(node.right, Math.max(min, data), max);
}
```

Time complexity: O(n)<br/>
Space complexity: O(n)
