2022-06-05 16:44
Tags: [[LeetCode]] - [[Depth First Search]] - [[Topological Sort]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Questions
- Input: Number of courses, prerequisites `int[][]`  array. To take course `prerequisites[0]`, we must first take `prerequisites[1]` 
- Output: Whether we have a valid schedule.

## Solution
Basically, check if there is cycle / Graph is a DAG.

### Post-order DFS
- Use [[Backtracking]] for the recursive stack.
```Java
class Solution {
    private boolean[] visited; // keep track of visted non-cyclic node
    private HashMap<Integer, LinkedList<Integer>> graph;
    
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        visited = new boolean[numCourses];
        
        // 1. build graph of prerequisites
        graph = new HashMap<>();
        for (int i = 0; i < prerequisites.length; i++) {
            int a = prerequisites[i][0];
            int b = prerequisites[i][1];
            if (!graph.containsKey(a)) graph.put(a, new LinkedList<>());
            graph.get(a).add(b);
        }
        
        // 2. Perform postorder DFS on each course. If there is a cycle, return false
        boolean[] traced = new boolean[numCourses]; // breadcrumbs, keep track of recursive stack
        for (int course : graph.keySet()) {
            if (isCycle(course, traced)) return false;
        }
        return true;
    }
    
    // return true if there is a cycle, else false
    public boolean isCycle(int i, boolean[] traced) {
        // if alr visited and non-cyclic, return false;
        if (visited[i]) return false;
        
        // if node is alr in recursive stack, return true;
        if (traced[i]) return true;
        
        // if no neighbour (leaf node), return false
        if (!graph.containsKey(i)) return false;
        
        // recursively check neighbors is a cycle
        traced[i] = true; // leave breadcrump
        boolean res = false;
        for (int neighbor : graph.get(i)) {
            res = isCycle(neighbor, traced);
            if (res) break;    
        }
        traced[i] = false; // remove breadcrump
        visited[i] = true;
        return res;
    }
}
```

Time: O(E + V) - traverse graph, visit each edge and node only once due to DFS
Space: O(E +V) - build graph takes E + V, 2 array of V space, recursion stack of V depth

### Topological Order
Do a topological sort, remove edges on the way. If the number of edges removed != total number of edges (hence, unremoved edges), there is cyclic dependencies.

Time: O(V + E)
- O(E) to build graph (traverse thru prerequisites)
- O(V + E) for Kahn (check every node and edge once since we only add 0-inDegree nodes)

Space: O(V + E)
- Graph takes O(V + E) space
- Queue max size is O(V) 

```Java
class Solution {
    private HashMap<Integer, Node> graph;
    
    private class Node {
        private Integer inDegrees = 0;
        private List<Node> outNeighbors = new LinkedList<>();
    } 
    
    public Node createGraph(int num) {
        if (!graph.containsKey(num)) {
            graph.put(num, new Node());
        }
        return graph.get(num);
    }
    
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (prerequisites.length == 0 || prerequisites.length == 1) 
            return true;
        
        graph = new HashMap<>();
        // build graph
        for (int[] edge : prerequisites) {
            Node preCourse = createGraph(edge[1]);
            Node subCourse = createGraph(edge[0]);
            preCourse.outNeighbors.add(subCourse);
            subCourse.inDegrees++;
        }
        
        // Kahn Algo
        int totalEdges = prerequisites.length;
        int edgesRemoved = 0;
        Queue<Node> S = new LinkedList<>(); // set of nodes w/ no incoming edges
        
        // 1. Add all nodes with no incoming edges
        for (Node node : graph.values()) {
            if (node.inDegrees == 0) {
                S.offer(node);
            }
        }
        
        // run Kahn
        while (!S.isEmpty()) {
            Node currNode = S.poll();
            for (Node neighbor : currNode.outNeighbors) {
                neighbor.inDegrees--;
                edgesRemoved++;
                if (neighbor.inDegrees == 0) {
                    S.offer(neighbor);
                }
            }
        }
        
        return edgesRemoved == totalEdges;
    }
}
```

