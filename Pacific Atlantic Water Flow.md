2022-06-05 16:44
Tags: [[LeetCode]] - [[Number of Islands]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Pacific Atlantic Water Flow
### Questions
**Input:** 2D int array, showing the height level of island at coordinate m x n. Water can flow from higher island to lower island.

![[Pasted image 20220618160557.png]]

**Output:** List of coordinates of island in which water can flow to both Pacific and Atlantic Ocean 

### Solution
Idea: Do BFS/DFS at the cells adjacent to each ocean. If it is reachable from both ocean, add to result.

##### [[Breadth First Search]]

```Java
class Solution {
    private static final int[][] DIRECTIONS = new int[][]{{0, 1}, {1, 0}, {-1, 0}, {0, -1}};
    private static final int Pacific = 0;
    private static final int Atlantic = 1;
    private int rows = 0;
    private int cols = 0;
    private int[][] matrix;
    
    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        rows = heights.length; cols = heights[0].length;
        matrix = heights;
        boolean[][][] visited = new boolean[rows][cols][2];
        List<List<Integer>> res = new ArrayList<>();
        
        // 1.BFS on nodes adjacent to Pacific Ocean and Atlantic Ocean
        for (int c = 0; c < cols; c++) {
            BFS(visited, 0, c, Pacific);
            BFS(visited, rows - 1, c, Atlantic);
        }
        
        for (int r = 0; r < rows; r++) {
            BFS(visited, r, 0, Pacific);
            BFS(visited, r, cols - 1, Atlantic);
        }        
        
        // 2.Check which node is visited twice, using an int[]
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (visited[r][c][0] && visited[r][c][1]) {
                    res.add(List.of(r, c));
                }
            }
        }
        return res;
    }
    
    public void BFS(boolean[][][] visited, int r, int c, int ocean) {
        if (visited[r][c][ocean] == true) {
            return;
        }
        LinkedList<Integer> frontier = new LinkedList<>();
        frontier.add(r * cols + c);
        visited[r][c][ocean] = true;
        while (!frontier.isEmpty()) {
            int coordinate = frontier.remove();
            int xCoord = coordinate / cols;
            int yCoord = coordinate % cols;
            int height = matrix[xCoord][yCoord];
            for (int[] dir : DIRECTIONS) {
                int x = xCoord + dir[0];
                int y = yCoord + dir[1];
                if (x < 0 || x >= rows || y < 0 || y >= cols) {
                    continue;
                }
                if (matrix[x][y] < height) {
                    continue;
                }
                if (visited[x][y][ocean] == true) {
                    continue;
                }
                visited[x][y][ocean] = true;
                frontier.add(x * cols + y);
            }
        }
    }
} 
```
Time: O($M * N$), worst case when all cells are equal, has to visit all $M * N$ cells twice
Space: O($M * N$). Space is from visited array + queue. Visited array costs O(2MN). Queue will never take more than O(MN) space 

##### [[Depth First Search]]

```Java
class Solution {
    private static final int[][] DIRECTIONS = new int[][]{{0, 1}, {1, 0}, {-1, 0}, {0, -1}};
    private int numRows;
    private int numCols;
    private int[][] landHeights;
    
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        // Check if input is empty
        if (matrix.length == 0 || matrix[0].length == 0) {
            return new ArrayList<>();
        }
        
        // Save initial values to parameters
        numRows = matrix.length;
        numCols = matrix[0].length;
        landHeights = matrix;
        boolean[][] pacificReachable = new boolean[numRows][numCols];
        boolean[][] atlanticReachable = new boolean[numRows][numCols];
        
        // Loop through each cell adjacent to the oceans and start a DFS
        for (int i = 0; i < numRows; i++) {
            dfs(i, 0, pacificReachable);
            dfs(i, numCols - 1, atlanticReachable);
        }
        for (int i = 0; i < numCols; i++) {
            dfs(0, i, pacificReachable);
            dfs(numRows - 1, i, atlanticReachable);
        }
        
        // Find all cells that can reach both oceans
        List<List<Integer>> commonCells = new ArrayList<>();
        for (int i = 0; i < numRows; i++) {
            for (int j = 0; j < numCols; j++) {
                if (pacificReachable[i][j] && atlanticReachable[i][j]) {
                    commonCells.add(List.of(i, j));
                }
            }
        }
        return commonCells;
    }
    
    private void dfs(int row, int col, boolean[][] reachable) {
        // This cell is reachable, so mark it
        reachable[row][col] = true;
        for (int[] dir : DIRECTIONS) { // Check all 4 directions
            int newRow = row + dir[0];
            int newCol = col + dir[1];
            // Check if new cell is within bounds
            if (newRow < 0 || newRow >= numRows || newCol < 0 || newCol >= numCols) {
                continue;
            }
            // Check that the new cell hasn't already been visited
            if (reachable[newRow][newCol]) {
                continue;
            }
            // Check that the new cell has a higher or equal height,
            // So that water can flow from the new cell to the old cell
            if (landHeights[newRow][newCol] < landHeights[row][col]) {
                continue;
            }
            // If we've gotten this far, that means the new cell is reachable
            dfs(newRow, newCol, reachable);
        }
    }
}
```