2022-06-05 16:44
Tags: [[LeetCode]] - [[Depth First Search]] - [[Breadth First Search]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Questions
Input: 2D m x n grid of '1' and '0' (1 and 0 matrix).

Output: Number of islands (an island consists of all the 1s connecting vertically and horizontally).

## Solution
The solutions below modify input, which is considered bad practice. It's better practice to keep a visited `boolean[][]` array instead. 

### [[Depth First Search]] approach: 

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:

        # base case:
        if not grid or not grid[0]:
            return 0
        # Max rows and columns
        ROWS, COLS = len(grid), len(grid[0])
        # visited set
        visited = [[False] * COLS for _ in range(ROWS)]
        # island count
        count = 0
        
        # directions
        DIR = [
            [-1, 0], # north
            [1, 0],  # south
            [0, 1],  # east
            [0, -1]  # west
        ]
        
        # dfs helper function
        def dfs(x, y):
            if x >= 0 and y >= 0 and x < ROWS and y < COLS:
                if visited[x][y] or grid[x][y] == '0':
                    return

                visited[x][y] = True
                for direction in DIR:
                    dfs(x + direction[0], y + direction[1])
        
        # do dfs on each entry
        for x in range(ROWS):
            for y in range(COLS):
                if not visited[x][y] and grid[x][y] != '0':
                    count += 1
                    dfs(x, y)
            
        return count
```

Time: O(m x n): DFS + check matrix
Space: O(m x n) if matrix is filled with 1s, then recursion goes m x n deep

![[Number of Island 2022-06-16 13.54.39.excalidraw]]

### [[Breadth First Search]] approach - BETTER SPACE COMPLEXITY
![[Pasted image 20220616135058.png]]

- Same time complexity, but space is reduced to `O(min(m, n))` , which is the max size of the [[Queue]] at any given time. 
- Linked List is uses as a [[Queue]].
- The Queue does not store Nodes, but an Integer value from which we can obtain the coordinate of the node!

```Java
class Solution {
  public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
      return 0;
    }

    int nr = grid.length;
    int nc = grid[0].length;
    int num_islands = 0;

    for (int r = 0; r < nr; ++r) {
      for (int c = 0; c < nc; ++c) {
        if (grid[r][c] == '1') {
          ++num_islands;
          grid[r][c] = '0'; // mark as visited
          Queue<Integer> neighbors = new LinkedList<>();
          
          neighbors.add(r * nc + c);
          while (!neighbors.isEmpty()) {
            int id = neighbors.remove();
            int row = id / nc;
            int col = id % nc;
            
            if (row - 1 >= 0 && grid[row-1][col] == '1') {
              neighbors.add((row-1) * nc + col);
              grid[row-1][col] = '0';
            }
            
            if (row + 1 < nr && grid[row+1][col] == '1') {
              neighbors.add((row+1) * nc + col);
              grid[row+1][col] = '0';
            }
            
            if (col - 1 >= 0 && grid[row][col-1] == '1') {
              neighbors.add(row * nc + col-1);
              grid[row][col-1] = '0';
            }
            
            if (col + 1 < nc && grid[row][col+1] == '1') {
              neighbors.add(row * nc + col+1);
              grid[row][col+1] = '0';
            }
          }
        }
      }
    }
    
    return num_islands;
  }
}
```

### [[Union-Find]] approach:

```Java
class Solution {
  class UnionFind {
    int count; // # of connected components
    int[] parent;
    int[] rank;

    public UnionFind(char[][] grid) { // initialise individual components
      count = 0;
      int m = grid.length;
      int n = grid[0].length;
      parent = new int[m * n];
      rank = new int[m * n];
      for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
          if (grid[i][j] == '1') {
            parent[i * n + j] = i * n + j;
            ++count;
          }
          rank[i * n + j] = 0;
        }
      }
    }

    public int find(int i) { // path compression
      if (parent[i] != i) parent[i] = find(parent[i]);
      return parent[i];
    }

    public void union(int x, int y) { // union with rank
      int rootx = find(x);
      int rooty = find(y);
      if (rootx != rooty) {
        if (rank[rootx] > rank[rooty]) {
          parent[rooty] = rootx;
        } else if (rank[rootx] < rank[rooty]) {
          parent[rootx] = rooty;
        } else {
          parent[rooty] = rootx; rank[rootx] += 1;
        }
        --count;
      }
    }

    public int getCount() {
      return count;
    }
  }

  public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
      return 0;
    }

    int nr = grid.length;
    int nc = grid[0].length;
    int num_islands = 0;
    UnionFind uf = new UnionFind(grid);
    for (int r = 0; r < nr; ++r) {
      for (int c = 0; c < nc; ++c) {
        if (grid[r][c] == '1') {
          grid[r][c] = '0';
          if (r - 1 >= 0 && grid[r-1][c] == '1') {
            uf.union(r * nc + c, (r-1) * nc + c);
          }
          if (r + 1 < nr && grid[r+1][c] == '1') {
            uf.union(r * nc + c, (r+1) * nc + c);
          }
          if (c - 1 >= 0 && grid[r][c-1] == '1') {
            uf.union(r * nc + c, r * nc + c - 1);
          }
          if (c + 1 < nc && grid[r][c+1] == '1') {
            uf.union(r * nc + c, r * nc + c + 1);
          }
        }
      }
    }

    return uf.getCount();
  }
}
```

Time and Space: O(m x n) to create data structure (union and find operation should take approximately constant time if both path compression and weighted union are implemented)