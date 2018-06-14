# Problem
https://www.hackerrank.com/challenges/ctci-connected-cell-in-a-grid/problem

# Solution
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
        region += getRegion(grid, x, y - 1, maxX, maxY);
        region += getRegion(grid, x - 1, y, maxX, maxY);
        region += getRegion(grid, x + 1, y - 1, maxX, maxY);
        region += getRegion(grid, x - 1, y - 1, maxX, maxY);
        region += getRegion(grid, x - 1, y + 1, maxX, maxY);
        region += getRegion(grid, x, y + 1, maxX, maxY);
        region += getRegion(grid, x + 1, y, maxX, maxY);
        region += getRegion(grid, x + 1, y + 1, maxX, maxY);
        return region;
    }
```
