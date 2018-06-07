# Problem
https://www.hackerrank.com/challenges/equal-stacks/problem
```
세 개의 스택이 주어지고, 각 스택에는 다른 높이의 실린더들이 들어있다.
세 스택의 높이가 같아지는 경우들 중, 높이의 maximum 값을 리턴하라.
세 스택의 높이는 각각 n1, n2, n3이다.
```

# Solution 
- 축적된 heights를 stack에 넣는다.
- 세 stack의 top value가 같다면, 그 값을 리턴한다. 
- 같지 않다면, 각 top value이 세 values의 minimum 값보다 크지 않을 때까지 pop.
- 세 stack 중 하나라도 empty stack이 된다면, 0을 리턴하면 된다.

```java
int equalStacks(int[] h1, int[] h2, int[] h3) {
    Stack<Integer> ac1 = getAccumulatedHeights(h1);
    Stack<Integer> ac2 = getAccumulatedHeights(h2);
    Stack<Integer> ac3 = getAccumulatedHeights(h3);

    while(!ac1.isEmpty() && !ac2.isEmpty() && !ac3.isEmpty()) {
        int ach1 = ac1.peek();
        int ach2 = ac2.peek();
        int ach3 = ac3.peek();
        
        if (ach1 == ach2 && ach2 == ach3) {
            return ach1;
        }
        
        int maxEqualHeight = Math.min(Math.min(ach1, ach2), ach3);

        while(!ac1.isEmpty() && ac1.peek() > maxEqualHeight) {
            ac1.pop();
        }
        while(!ac2.isEmpty() && ac2.peek() > maxEqualHeight) {
            ac2.pop();
        }
        while(!ac3.isEmpty() && ac3.peek() > maxEqualHeight) {
            ac3.pop();
        }
    }
    
    return 0;
}

private Stack<Integer> getAccumulatedHeights(int[] heights) {
    Stack<Integer> stack = new Stack<Integer>();
    int accumulated = 0;

    for(int i = heights.length - 1; i >= 0; --i) {
        int e = heights[i];
        accumulated += e;
        stack.push(accumulated);
    }
    
    return stack;    
}
```

Time complexity: O(n1+n2+n3)<br/>
Space complexity: O(n1+n2+n3)
