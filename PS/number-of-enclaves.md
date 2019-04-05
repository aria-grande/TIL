# Problem
https://leetcode.com/problems/number-of-enclaves/

Given a 2D array A, each cell is 0 (representing sea) or 1 (representing land)

A move consists of walking from one land square 4-directionally to another land square, or off the boundary of the grid.

Return the number of land squares in the grid for which we cannot walk off the boundary of the grid in any number of moves.

# Solution
DFS를 활용하여 풀어보았다.
```java
public int numEnclaves(int[][] arr) {
        final int ROW = arr.length;
        final int COL = arr[0].length;
        Queue<Integer> xs = new LinkedList<>();
        Queue<Integer> ys = new LinkedList<>();
        // horizontal
        for(int c = 0; c < COL; ++c) {
            if(arr[0][c] == 1) {
                xs.add(0);
                ys.add(c);
            }
            if(arr[ROW - 1][c] == 1) {
                xs.add(ROW - 1);
                ys.add(c);
            }
        }
        // vertical
        for(int r = 1; r < ROW - 1; ++r) {
            if(arr[r][0] == 1) {
                xs.add(r);
                ys.add(0);
            }
            if(arr[r][COL - 1] == 1) {
                xs.add(r);
                ys.add(COL - 1);
            }
        }
        
        while(xs.peek() != null && ys.peek() != null) {
            int x = xs.poll();
            int y = ys.poll();
            arr[x][y] = 0;
            
            if(x >= 1 && x < ROW && arr[x - 1][y] == 1) {
                xs.add(x - 1);
                ys.add(y);
            }
            if(y >= -1 && y < COL - 1 && arr[x][y + 1] == 1) {
                xs.add(x);
                ys.add(y + 1);
            }
            if(y >= 1 && y < COL + 1 && arr[x][y - 1] == 1) {
                xs.add(x);
                ys.add(y - 1);
            }
            if(x >= -1 && x < ROW - 1 && arr[x + 1][y] == 1) {
                xs.add(x + 1);
                ys.add(y);
            }
        }
        
        int lands = 0;
        for(int row = 1; row < ROW - 1; ++row) {
            for(int col = 1; col < COL - 1; ++col) {
                if(arr[row][col] == 1) {
                    lands++;
                }
            }
        }
        return lands;
    }
```
[200][201]의 배열에 대해서 Time limit이 발생한다.
왜 그럴까?
