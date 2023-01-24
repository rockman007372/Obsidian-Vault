2022-07-26 22:13
Tags: [[LeetCode]] - [[Topological Sort]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Alien Dictionary
### My Performance

### Questions
Difficulty: #hard 
Input: `String[]` containing words in lexicographically increasing order.
Output: A `String` containing the letters in lexicographically increasing order.

### Solution
##### Kahn's Algorithm
Time: 
- Let N be the number of words
- C be the TOTAL number of characters
- U be the number of UNIQUE characters
- Creating dependency takes O(C) as we have to compare every single character
- O(V + E) to do topo sort using Kahn algorithm, because each edge is removed once and each node is visited once after we remove all of its incoming edges.
- V = U
- E = O(N - 1) because each pair of words yields exactly one edge
- E = O($U^2$) because there is at most 1 edge between nodes, hence at most we have (U + U - 1 + U - 2 + ...) edges
- E = O(Min($U^2$, N - 1))
- Total: O(C + U + Min($U^2$, N - 1)) = O(C) since C > U >= N

Space: O(1) or O(U + Min($U^2$, N - 1))
- O(1) if we take U = 26

```Java
class Solution {
    private HashMap<Character, LinkedList<Character>> adjList;
    private HashMap<Character, Integer> inDegree;
    
    public String alienOrder(String[] words) {
        // extract dependecies from words
        // and add directed edges to adjList
        createGraph(words);
        
        // if the prefix comes after -> invalid
        // eg: abcf, abc
        if (adjList == null) return "";
        
        // Kahns Algorithm to establish topo order,
        // also check for cycles 
        return kahns();
    }
    
    private String kahns() {
        StringBuilder sb = new StringBuilder();
        Queue<Character> queue = new LinkedList<>();
        
        // add char with 0 indegrees to queue
        for (Map.Entry<Character, Integer> charSet : inDegree.entrySet()) {
            if (charSet.getValue() == 0) {
                char c = charSet.getKey();
                queue.offer(c);
                sb.append(c);
            }
        }
        
        // remove the outgoing edges, add new zero-indegree chars
        while (!queue.isEmpty()) {
            char curr = queue.poll();
            for (char neighbor : adjList.get(curr)) {
                int newDegree = inDegree.get(neighbor) - 1;
                inDegree.put(neighbor, newDegree);
                if (newDegree == 0) {
                    queue.offer(neighbor);
                    sb.append(neighbor);
                }
            }
        }
        
        // if some char is not visited, there must be a cycle
        return sb.length() < adjList.size() ? "" : sb.toString();
    }
    
    private void createGraph(String[] words) {
        this.adjList = new HashMap<>();
        this.inDegree = new HashMap<>();
        
        // find all unique letters
        for (String word : words) {
            for (int i = 0, n = word.length(); i < n; i++) {
                adjList.put(word.charAt(i), new LinkedList<>());
                inDegree.put(word.charAt(i), 0);
            }
        }
        
        int len = words.length;
        for (int i = 0; i < len - 1; i++) {
            String word1 = words[i];
            String word2 = words[i + 1];
            
            // if the prefix comes after -> invalid
            // eg: abcf, abc
            if (word1.length() > word2.length() && word1.startsWith(word2)) {
                adjList = null;
                return;
            }
            
            // find the first different characters and 
            // extract dependency
            int maxLen = Math.min(word1.length(), word2.length());
            for (int j = 0; j < maxLen; j++) {
                char c1 = word1.charAt(j);
                char c2 = word2.charAt(j);
                if (c1 != c2) {
                    adjList.get(c1).add(c2);
                    inDegree.put(c2, inDegree.get(c2) + 1);
                    break;
                }
            }
        }   
    }
}
```

##### Post-Order DFS

```Java
class Solution {
    private HashMap<Character, LinkedList<Character>> adjList;
    private HashSet<Character> visited;
    private HashSet<Character> stack;
    
    public String alienOrder(String[] words) {
        // extract dependecies from words
        // and add directed edges to adjList
        createGraph(words);
        
        // if the prefix comes after -> invalid
        // eg: abcf, abc
        if (adjList == null) return "";
        
        // PostOrder DFS to establish topo order,
        // also check for cycles
        StringBuilder sb = new StringBuilder();
        visited = new HashSet<>();
        stack = new HashSet<>();
        for (Character c : adjList.keySet()) {
            if (!visited.contains(c)) {
                if (!dfs(sb, c)) {
                    return "";
                }    
            }
        }
        return sb.reverse().toString();
    }
    
    // return true iff no cycles detected
    private boolean dfs(StringBuilder sb, Character c) { 
        visited.add(c); // mark c as visited
        
        stack.add(c); // add c to the current recursion stack
        boolean noCycle = true;
        for (Character neighbor : adjList.get(c)) {
            // if we see a neighbor in the recursion stack,
            // a cycle is detected
            if (stack.contains(neighbor)) {
                noCycle = false;
                break;
            }   
            
            if (!visited.contains(neighbor)) {
                if (!dfs(sb, neighbor)) {
                    noCycle = false;
                    break;
                }  
            }
        }
        stack.remove(c); // remove breadcrumps
        sb.append(c); // post-order 
        return noCycle;
    }
    
	// A cleaner version using HashMap to store the boolean
	// whether a visited node has a cycle or not.
    private boolean dfs(Character c) {
        if (seen.containsKey(c)) {
            return seen.get(c); // If this node was grey (false), a cycle was detected.
        }
        seen.put(c, false);
        for (Character next : reverseAdjList.get(c)) {
            boolean result = dfs(next);
            if (!result) return false;
        }
        seen.put(c, true);
        output.append(c);
        return true;
    }
    
    private void createGraph(String[] words) {
        this.adjList = new HashMap<>();
        
        // find all unique letters
        for (String word : words) {
            for (int i = 0, n = word.length(); i < n; i++) {
                adjList.put(word.charAt(i), new LinkedList<>());
            }
        }
        
        int len = words.length;
        for (int i = 0; i < len - 1; i++) {
            String word1 = words[i];
            String word2 = words[i + 1];
            
            // if the prefix comes after -> invalid
            // eg: abcf, abc
            if (word1.length() > word2.length() && word1.startsWith(word2)) {
                adjList = null;
                return;
            }
            
            // find the first different characters and 
            // extract dependency
            int maxLen = Math.min(word1.length(), word2.length());
            for (int j = 0; j < maxLen; j++) {
                char c1 = word1.charAt(j);
                char c2 = word2.charAt(j);
                if (c1 != c2) {
                    adjList.get(c1).add(c2);
                    break;
                }
            }
        }   
    }
}

```