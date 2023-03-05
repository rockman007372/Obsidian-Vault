2022-06-05 16:44
Tags: [[LeetCode]] - [[Depth First Search]] - [[Breadth First Search]] - [[Hash Table]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Questions
Input: a root node of a graph (implemented as a adjacency list)
```Java
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
```

Output: A deep copy of the node

### Solution
#### Depth First Search
```Java
class Solution {
    public HashMap<Integer, Node> copied = new HashMap<>();
    public Node cloneGraph(Node node) {
        // handle base cases
        if (node == null || node.neighbors == null) return node;
        
        int val = node.val;
        
        // 1. if node is alr copied, return node
        if (copied.containsKey(val)) return copied.get(val);
        
        // 2. else, clone new node and new neighbour
        Node root = new Node(node.val);        
        List<Node> neighbors = new ArrayList<>();
        root.neighbors = neighbors;
            
        // 3. add copied root to the hashmap
        copied.put(val, root);
        
        // 4. go through the original neighbour list to add nodes
        for (Node neighbor : node.neighbors) {
            root.neighbors.add(cloneGraph(neighbor));    
        }
        
        return root;
    }
}
```

Time: O(V + E) to traverse the whole graph
Space: O(V) for hashmap and recursion depth

#### Breadth First Search

```Java
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) {
            return node;
        }

        // Hash map to save the visited node and it's respective clone
        // as key and value respectively. This helps to avoid cycles.
        HashMap<Node, Node> visited = new HashMap();

        // Put the first node in the queue
        LinkedList<Node> queue = new LinkedList<Node> ();
        queue.add(node);
        // Clone the node and put it in the visited dictionary.
        visited.put(node, new Node(node.val, new ArrayList()));

        // Start BFS traversal
        while (!queue.isEmpty()) {
            // Pop a node say "n" from the from the front of the queue.
            Node n = queue.remove();
            // Iterate through all the neighbors of the node "n"
            for (Node neighbor: n.neighbors) {
                if (!visited.containsKey(neighbor)) {
                    // Clone the neighbor and put in the visited, if not present already
                    visited.put(neighbor, new Node(neighbor.val, new ArrayList()));
                    // Add the newly encountered node to the queue.
                    queue.add(neighbor);
                }
                // Add the clone of the neighbor to the neighbors of the clone node "n".
                Node nClone = visited.get(n);
                Node neighborClone = visited.get(neighbor); 
                nClone.neighbors.add(neighborClone);
            }
        }

        // Return the clone of the node from visited.
        return visited.get(node);
    }
}
```