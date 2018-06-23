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


## without recursion
Stack을 활용하여, 노드의 left subtree - 자신 - right subtree를 push 한다.

```java
void traverse(Node root) {
  if (root == null) {
    return ;
  }
  
  Stack<Node> stack = new Stack<Node>();
  StringBuilder sb = new StringBuilder();
  
  /* push left nodes */
  Node leftNode = root;
  while(leftNode != null) {
    stack.push(leftNode);
    leftNode = leftNode.left;
  }
  
  /* pop and print */
  while(!stack.isEmpty()) {
    Node node = stack.pop();
    sb.append(node.data + " ");
    
    /* check if node has right subtree */
    if (node.right != null) {
      Node rightSubtree = node.right;
      while(rightSubtree != null) {
        stack.push(rightSubtree);
        rightSubtree = rightSubtree.left;
      }
    }
  }
  
  System.out.println(sb.toString().trim());
}
```

n이 노드의 갯수일때,<br/>
Time complexity: O(n)<br/>
Space complexity: O(n)

## 참고 링크
- [Tree traversal](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)
