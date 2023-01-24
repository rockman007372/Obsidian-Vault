2022-07-15 10:54
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Number of Connected Components in an Undirected Graph
### My Performance
#complete #onTime 
### Questions
Difficulty: #medium 
Input: edge array and number of nodes
Output: number of connected components

### Solution

##### Iterative DFS - [[Depth First Search]]

Time: O(V + E) - O(E) to create adjList, O(V) to visit each node once.
Space: O(V + E)
```Java
class Solution {
    private HashMap<Integer, LinkedList<Integer>> adjList;
    private HashSet<Integer> visited;
    
    public int countComponents(int n, int[][] edges) {
        int count = 0;
        adjList = new HashMap<>();
        visited = new HashSet<>();
        
        for (int i = 0; i < n; i++) {
            adjList.put(i, new LinkedList<>());
        }
        for (int[] edge : edges) {
            int a = edge[0];
            int b = edge[1];
            adjList.get(a).add(b);
            adjList.get(b).add(a);
        }
        
        for (int i = 0; i < n; i++) {
            if (!visited.contains(i)) {
                count++; // we find another component
                dfs(i);
            }
        }
        
        return count;
    }
    
    public void dfs(int i) {
        if (!visited.contains(i)) {            
            // dfs from the root node
            Stack<Integer> stack = new Stack<>();
            visited.add(i);
            stack.push(i);
            while (!stack.isEmpty()) {
                int curr = stack.pop();
                for (int neighbor : adjList.get(curr)) {
                    if (!visited.contains(neighbor)) {
                        visited.add(neighbor);
                        stack.push(neighbor);
                    }
                }
            }
        }
    }
}
```

##### Union-Find
[[Union-Find]]: Whevever union happens, decrement # connected components by 1.

Time: O(V + E) - O(V to initialise UnionFind, O(E) to iterate through each edge for union.
Space: O(V) to store UF

```Java
class Solution {
    private class UnionFind {
        private int[] parents;
        private int [] size;
        private int connectedComponents;
        
        private UnionFind(int n) {
            parents = new int[n];
            size = new int[n];
            connectedComponents = n;
            for (int i = 0; i < n; i++) {
                parents[i] = i;
                size[i] = 1;
            }
        }
        
        private int findRoot(int i) {
            if (parents[i] != i) parents[i] = findRoot(parents[i]);
            return parents[i];
        }
        
        private void union(int i, int j) {
            int parentI = findRoot(i);
            int parentJ = findRoot(j);
            
            if (parentI != parentJ) {
                connectedComponents--; // decrement components by one if union happens
                if (size[parentI] < size[parentJ]) {
                    parents[parentI] = parentJ;
                    size[parentJ] += size[parentI];
                } else {
                    parents[parentJ] = parentI;
                    size[parentI] += size[parentJ];
                }
            }
        }
    }
    
    public int countComponents(int n, int[][] edges) {
        UnionFind uf = new UnionFind(n);
        for (int[] edge : edges) {
            uf.union(edge[0], edge[1]);
        }
        return uf.connectedComponents;
    }
}
```