2022-06-05 16:44
Tags: [[LeetCode]] - [[Trie]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Design Add and Search Words Data Structure
### My Performance
Alright, I need to review the code I wrote in CS2040S to have a direction.
#complete #notOnTime

### Questions
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

-   `WordDictionary()` Initializes the object.
-   `void addWord(word)` Adds `word` to the data structure, it can be matched later.
-   `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

### Solution
addWord:
Time: O(M), M is the length of the search word
Space: O(1)

search:
Time: O(M) if no wildcard, O($26^M$) in the worst case: `......z`
Space: O(1) if no wildcard, O(M) in worst case (deepest recursion depth)

```Java
class WordDictionary {
    private Node rootNode; 
    private static final Node TERMINAL = new Node();
    private static final char WILDCARD = '.';
    
    private static class Node {
        private char character;
        private Node[] children = new Node[27];
        
        public Node() {};
        
        public Node(char character) {
            this.character = character;
        }
        
        public void addChild(char character) {
            int index = WordDictionary.charToInt(character);
            if (children[index] == null) {
                children[index] = new Node(character);                
            }
        }
        
        public Node getChild(char character) {
            return children[WordDictionary.charToInt(character)];
        }
        
        public boolean containChild(char character) {
            return children[WordDictionary.charToInt(character)] != null;
        }
        
        public void terminate() {
            children[26] = TERMINAL;
        }
        
        public boolean isTerminated() {
            return children[26] == TERMINAL;
        }
        
        public int childrenLength() {
            return 26;
        }
        
        public Node childAt(int index) {
            return children[index];
        }
    }
    
    public static int charToInt(char c) {
        return c - 97;
    }
    
    public WordDictionary() {
        rootNode = new Node();    
    }
    
    public void addWord(String word) {
        Node current = this.rootNode;
        for (int i = 0, n = word.length() ; i < n ; i++) { 
            char c = word.charAt(i);
            current.addChild(c);
            current = current.getChild(c);
        }
        current.terminate();  
    }
    
    public boolean search(String word) {
        return searchHelper(word, 0, this.rootNode);
    }
    
    public boolean searchHelper(String word, int index, Node curr) {
        for (int i = index, n = word.length(); i < n; i++) {
            char c = word.charAt(i);
            
            // if wildcard, check every single child
            if (c == WILDCARD) {
                for (int j = 0; j < curr.childrenLength(); j++) {
                    Node child = curr.childAt(j);
                    if (child == null) continue;
                    
                    if (searchHelper(word, i + 1, child)) {
                        return true;
                    }                    
                }
                 
                // if current node has no children
                return false;
            }
            
            // if not wildcard, search normally
            if (!curr.containChild(c)) return false;
            curr = curr.getChild(c);
        }
           
        // reach last node, check if terminated                
        return curr.isTerminated(); 
    }
}

```
