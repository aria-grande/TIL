# Problem
There a map given as `lot`, a list of lists of integers, that each values contains 0 or 1. 
0 means not a way be able to pass through, and 1 means a way be able to pass through.
Find the shortest distance from (0, 0) to (destX, destY). 

# Solution

```java
public class Solution {        
    int removeObstacle(int numRows, int numColumns, List<List<Integer>> lot, int destX, int destY) {
        // set visited values
        boolean[][] visited = new boolean[numRows][numColumns];
        for(int i = 0; i < numRows; ++i) {
            List<Integer> row = lot.get(i);
            for(int j = 0; j < numColumns; ++j) {
                int data = row.get(j);
                visited[i][j] = (data == 0);
            }
        }
        
        // find thes shortest distance
        Queue<Cell> bfs = new LinkedList<Cell>();
        bfs.add(new Cell(0, 0, 0));
        visited[0][0] = true;
        
        while(bfs.peek() != null) {
            Cell cell = bfs.poll();
            // when meets obstacle
            if(cell.row == destY && cell.col == destX) {
                return cell.dist;
            }
            
            // when moves up 
            if(cell.row >= 1 && !visited[cell.row - 1][cell.col]) {
                bfs.add(new Cell(cell.row - 1, cell.col, cell.dist + 1));
                visited[cell.row - 1][cell.col] = true;
                
            }        
            // when moves down 
            if(cell.row < numRows - 1 && !visited[cell.row + 1][cell.col]) {
                bfs.add(new Cell(cell.row + 1, cell.col, cell.dist + 1));
                visited[cell.row + 1][cell.col] = true;
            }
            // when moves right 
            if(cell.col < numColumns - 1 && !visited[cell.row][cell.col + 1]) {
                bfs.add(new Cell(cell.row, cell.col + 1, cell.dist + 1));
                visited[cell.row][cell.col + 1] = true;
            }
            // when moves left
            if(cell.col >= 1 && !visited[cell.row][cell.col - 1]) {
                bfs.add(new Cell(cell.row, cell.col - 1, cell.dist + 1));
                visited[cell.row][cell.col - 1] = true;
            }
        }
        
        return -1;
    }
}

class Cell {
    int row;
    int col;
    int dist;
    
    public Cell(int row, int col, int dist) {
        this.row = row;
        this.col = col;
        this.dist = dist;
    }
}
```
