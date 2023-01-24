2022-07-07 18:33
Tags: [[LeetCode]] - [[Backtracking]] - [[Trie]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Word Search II
### My Performance
#uncomplete 

### Questions
Difficulty: #hard 
Input: `char[][]` board of characters, `String[]` array of words 
Output: the list of words that the board contains.

### Solution

##### Backtracing through the board while traversing a Trie 

Algorithm: 
- Add all the words to a trie -> WHY? We can search for all the words with the same prefix at the same time!
- Starting at each character in board, use backtracking to explore possible words as we traverse through the Trie. If word is containted in the Trie, add to result list.

Optimization:
- We can continuously trim the leaf node as we traverse through the Trie (If we have reached the leaf node, it means all words under this prefex has been added and we can thus trim it) -> Non-leaf nodes could become leaf nodes later, since we trim their children leaf nodes. -> Trie can be empty and we are done!
- Keep the word in TrieNode so we dont have to pass the prefix around in backtracking function

Time: O( $M * (4 * 3^{L-1})$ )
- M is the number of cells (rows x cols)
- L is the length of the longest word
- 4 is the initial number of directions we can explore
- $3^{L - 1}$ is the numbers of ways to explore every path afterwards

Space: O(N)
- N is the total number of letters in the dictionary (making up the words)

```Java
class Solution {
    private class TrieNode {
        public String word = null;
        public HashMap<Character, TrieNode> children = new HashMap<>();
    }
    
    private List<String> res;
    private char[][] board;
    private static final int[][] MOVES = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    
    public List<String> findWords(char[][] board, String[] words) {
        // 1. Build Trie
        TrieNode root = new TrieNode();
        for (String word : words) {
            TrieNode curr = root;
            for (int i = 0, n = word.length(); i < n; i++) {
                Character currChar = word.charAt(i);
                if (!curr.children.containsKey(currChar)) {
                    curr.children.put(currChar, new TrieNode());                    
                }
                curr = curr.children.get(currChar);
            }
            curr.word = word;
        }
        
        // 2. backtrack through Board and Trie to find words
        res = new ArrayList<>();
        this.board = board;
        for (int r = 0; r < board.length; r++) {
            for (int c = 0; c < board[0].length; c++) {
                // instead of having visited array, we can destroy
                // and reconstruct the board table;
                if (root.children.containsKey(board[r][c])) {
                    backtrack(r, c, root);                    
                }
            }
        }
        
        return res;
    }
    
    private void backtrack(int r, int c, TrieNode parent) {
        char currChar = board[r][c];
        TrieNode currNode = parent.children.get(currChar);
        
        // Found solution?
        if (currNode.word != null) {
            res.add(currNode.word);
            currNode.word = null; // prevent duplicates
        }
    
        // mark breadcrumb
        board[r][c] = '*';
        
        // traverse in possible directions
        for (int i = 0; i < MOVES.length; i++) {
            int nextRow = r + MOVES[i][0];
            int nextCol = c + MOVES[i][1];
            
            // check valid candidates
            if (nextRow < 0 || nextRow >= board.length 
                || nextCol < 0 || nextCol >= board[0].length) {
                continue;
            }
	        
	        if (currNode.children.containsKey(
		        board[nextRow][nextCol])) {
	            backtrack(nextRow, nextCol, currNode);    
	        }
        }
        
        // unmark breadcrumb
        board[r][c] = currChar;
        
        // prune Trie by recursively trimming the leaf nodes
        if (currNode.children.isEmpty()) {
            parent.children.remove(currChar);            
        }
    }
}
```