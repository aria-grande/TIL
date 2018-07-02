# Problem
https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/

```
주어진 2차원 정수 배열에 대해, 각 원소를 나선 방향으로 프린트하는 함수를 작성하시오.

(입력)
[[1, 2, 3],
 [8, 9, 4],
 [7, 6, 5]]
 
(출력) 1 2 3 4 5 6 7 8 9
```

# Solution
depth를 두고, 가장 외곽을 나선방향으로 돌아가면 된다. depth가 0이면 가장 외곽, 1이면 그 다음 외곽을 도는 것을 의미한다.<br/>
이 때, 주의할 점은 arr의 row와 column 갯수가 같지 않을 수도 있다는 것이다.

```java
void printSpirally(int[][] arr) {
  int row = arr.length;
  int col = arr[0].length;
  
  int x = 0; // col
  int y = 0; // row
  int depth = 0;
  int maxDepth = Math.max(row, col) / 2;
  while(depth <= maxDepth) {
    x += depth;
    y += depth;
    
    while(x < col - depth) {
      System.out.print(arr[y][x++] + " ");
    }
    x--;  // while문을 벗어났을 경우에는 array의 out bound에 index가 위치해있을 것이므로
    y++;  // 이미 프린트 한 원소는 다시 프린트 하지 않기 위해
    
    while(y < row - depth) {
      System.out.print(arr[y++][x] + " ");
    }
    y--;
    x--;

    while(x >= depth) {
      System.out.print(arr[y][x--] + " ");
    }
    x++;
    y--;

    while(y >= depth + 1) {
      System.out.print(arr[y--][x] + " ");
    }
    
    depth++;
  }
  System.out.println();
}
```

Time complexity: O(row * col)<br/>
Space complexity: O(1)
