# Problem
https://www.hackerrank.com/challenges/tree-inorder-traversal/problem
```
Complete the inOrder function, which has 1 parameter that is a pointer to the root of a binary tree and prints in order traversal.
```

# Solution

```java
void traverse(Node root) {
  inOrder(root);
}
void inOrder(Node node) {
  if(node == null) {
    return ;
  }
  inOrder(node.left);
  System.out.print(node.data + " ");
  inOrder(node.right);
}
```
n이 노드의 갯수일때,<br/>
Time complexity: O(n)<br/>
Space complexity: O(1) // 재귀 호출에 의한 스택도 카운트 한다면 O(n)
