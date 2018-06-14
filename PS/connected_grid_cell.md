# Problem
https://www.hackerrank.com/challenges/ctci-connected-cell-in-a-grid/problem

# Solution
[Depth first search](https://ko.wikipedia.org/wiki/%EA%B9%8A%EC%9D%B4_%EC%9A%B0%EC%84%A0_%ED%83%90%EC%83%89)를 이용하는 것이 핵심이다!<br/>
grid를 한번씩 훑는데, 이미 지나온 elements는 0으로 바꿔 여러 번 카운팅되지 않도록 한다.
```java
static int maxRegion(int[][] grid) {
    int maxY = grid.length - 1;
    int maxX = grid[0].length - 1;
    int max = 0;
    for(int x = 0; x <= maxX; ++x) {
        for(int y = 0; y <= maxY; ++y) {
            int region = getRegion(grid, x, y, maxX, maxY);
            max = Math.max(region, max);
        }
    }
    return max;
    }

static int getRegion(int[][] grid, int x, int y, int maxX, int maxY) {
    if (x < 0 || y < 0 || x > maxX || y > maxY || grid[y][x] == 0) {
        return 0;
    }
    int region = 1;
    grid[y][x] = 0;
    for(int row = y - 1; row <= y + 1; ++row) {
        for(int col = x - 1; col <= x + 1; ++col) {
            if (row != y || col != x) {
                region += getRegion(grid, col, row, maxX, maxY);    
            }
        }
    }
    return region;
}
```
grid의 원소의 갯수를 N개라 할 때,<br/>
Time complexity: O(N)<br/>
Space complexity: O(1)<br/>
