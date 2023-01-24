2022-07-10 11:07
Tags: [[LeetCode]] - [[Depth First Search]] - [[Breadth First Search]] - [[Course Schedule]] - [[Graph]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Graph Valid Tree
### My Performance
#complete #onTime 

### Questions
Difficulty: #medium 
Input: number of nodes and edges
Output: determine if its a valid tree

### Solution
```
/*
A tree: only 1 connected component, no cycle, E = V - 1

To check connected component: we can do one BFS/DFFS then iterate through all the nodes to see if any is unvisited

To check for cycle: E = V - 1, given graph is connected

- - -
We should create an adjacency list out of the edges array for easier DFS.
*/
```

##### Find Cycle in Undirected Graph Without Graph Theory
![[Pasted image 20220710111839.png]]
To find cycle in directed graphs, we just have to check for topo order (See [[Course Schedule]])
In undirected graph, we can run into trivial cycles as above. 

Hence, we can either delete the backward edge as we visit a forward edge. Or, we can create a parent map which maps a visited node to its direct parent. This allows us to check and prevent dfs/bfs from visiting the parent node, aka going backwards. If we still stumble accross a previous parent node, it means there must be a cycle!

```Java
// Use a map to keep track of how we got into each node.
Map<Integer, Integer> parent = new HashMap<>();
parent.put(0, -1);

// While there are nodes remaining on the stack...
while (!stack.isEmpty()) {
    int node = stack.pop(); // Take one off to visit.
    // Check for unseen neighbours of this node:
    for (int neighbour : adjacencyList.get(node)) {
        // Don't look at the trivial cycle.
        if (parent.get(node) == neighbour) {
            continue;
        }
        // Check if we've already seen this node.
        if (parent.containsKey(neighbour)) {
            return false; // There must be a cycle.
        }
        // Otherwise, put this neighbour onto stack
        // and record that it has been seen.
        stack.push(neighbour);
        parent.put(neighbour, node);
    }
}
```

##### Graph Theory + Recursive DFS
```Java
class Solution {
    private Set<Integer> visited;
    HashMap<Integer, LinkedList<Integer>> adjList;
    
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n - 1) return false;
        
        adjList = new HashMap<>();
        // create adjList
        for (int[] edge : edges) {
            int a = edge[0];
            int b = edge[1];
            if (!adjList.containsKey(a)) {
                adjList.put(a, new LinkedList<>());
            }
            
            if (!adjList.containsKey(b)) {
                adjList.put(b, new LinkedList<>());
            }
            
            adjList.get(a).add(b);
            adjList.get(b).add(a);
        }
        
        // perform dfs on root
        visited = new HashSet<>();
        dfs(0);
        
        // check for connected components
        return visited.size() == n;
    }
    
    private void dfs(int node) {
        visited.add(node);
        
        LinkedList<Integer> neighbors = adjList.get(node);
        if (neighbors == null) return;
        
        for (int neighbor : neighbors) {
            if (!visited.contains(neighbor)) {
                dfs(neighbor);
            }
        }
    }
}
```

Time: O(V + E) = O(V) since V = O(E)
Space: O(V + E) = O(V)

##### Iterative DFS
```Java
class Solution {
    private Set<Integer> visited;
    HashMap<Integer, LinkedList<Integer>> adjList;
    
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n - 1) return false;
        
        adjList = new HashMap<>();
        // create adjList
        for (int[] edge : edges) {
            int a = edge[0];
            int b = edge[1];
            if (!adjList.containsKey(a)) {
                adjList.put(a, new LinkedList<>());
            }
            
            if (!adjList.containsKey(b)) {
                adjList.put(b, new LinkedList<>());
            }
            
            adjList.get(a).add(b);
            adjList.get(b).add(a);
        }
        
        // perform dfs on root
        visited = new HashSet<>();
        dfs(0);
        
        // check for connected components
        return visited.size() == n;
    }
    
    private void dfs(int root) {
        Stack<Integer> stack = new Stack<>();
        stack.push(root);
        visited.add(root);
        while (!stack.isEmpty()) {
            Integer curr = stack.pop();
            LinkedList<Integer> neighbors = adjList.get(curr);
            if (neighbors == null) continue;
            for (int neighbor : neighbors) {
                if (visited.contains(neighbor)) {
                    continue;
                }
                stack.push(neighbor);
                visited.add(neighbor);
            }
        }   
    }
}
```

##### Union-Find
Using [[Union-Find]] to determine if the tree is connected / contains a single connected component. 

First we check if E = V - 1. This ensures there are enough edges to form one single connected component. 

Next we union every edge and check if theres a union operation that does not result in a merge. This means the 2 nodes are already in a connected component and unioning them will create a cycle. Hence graph is cyclic and not a tree.

```Java
class Solution {
    
    private class UnionFind {
        private int[] parent;
        private int[] size;
        
        private UnionFind(int n) {
            this.parent = new int[n];
            this.size = new int[n];
            Arrays.fill(size, 1);
            for (int i = 0; i < n; i++) {
                parent[i] = i;
            }
        }
        
        // Path Compression heuristics
        private int findRoot(int p) {
            if (p != parent[p]) parent[p] = findRoot(parent[p]);
            return parent[p];
        }
        
        private boolean find(int p, int q) {
            return findRoot(p) == findRoot(q);
        }
        
        // Weighted Union Heuristics
        private boolean union(int p, int q) {
            int rootP = findRoot(p);
            int rootQ = findRoot(q);
            
            if (rootP == rootQ) return false;
            
            if (size[rootP] > size[rootQ]) {
                parent[rootQ] = rootP;
                size[rootP] += size[rootQ];
            } else {
                parent[rootP] = rootQ;
                size[rootQ] += size[rootP];
            }
            return true;
        }
        
    }

    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n - 1) return false;
        
        UnionFind uf = new UnionFind(n);
        for (int[] edge : edges) {
            if (!uf.union(edge[0], edge[1])) {
                return false;
            }
        }
        return true;
    }
}
```