2022-07-01 16:13
Tags: [[Data Structure and Algorithm]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Trie
## Main Points
A Tree data structure for efficient implementation of dictionary.  

![[Pasted image 20220701161506.png]]

Time to search for a String: O(String.length)
Space to implement Trie: O(text size * Overheads)

##### Implementation
![[Pasted image 20220701161714.png]]


Assuming all characters are lowercased alphabets: 

```Java
class Trie {
    private Node rootNode; 
    private static Node TERMINAL = new Node();
    
    private static class Node {
        private char character;
        private Node[] children = new Node[28];
        
        public Node() {};
        
        public Node(char character) {
            this.character = character;
        }
        
        public void addChild(char character) {
            int index = Trie.charToInt(character);
            if (children[index] == null) {
                children[index] = new Node(character);                
            }
        }
        
        public Node getChild(char character) {
            return children[Trie.charToInt(character)];
        }
        
        public boolean containChild(char character) {
            return children[Trie.charToInt(character)] != null;
        }
        
        public void terminate() {
            children[26] = TERMINAL;
        }
        
        public boolean isTerminated() {
            return children[26] == TERMINAL;
        }
    }
    
    public static int charToInt(char c) {
        return c - 97;
    }
    
    public Trie() {
       this.rootNode = new Node((char) 123);
    }
    
    public void insert(String word) {
        Node current = this.rootNode;
        for (int i = 0, n = word.length() ; i < n ; i++) { 
            char c = word.charAt(i);
            current.addChild(c);
            current = current.getChild(c);
        }
        current.terminate();
    }
    
    public boolean search(String word) {
        Node current = this.rootNode;
        for (int i = 0, n = word.length() ; i < n ; i++) { 
            char c = word.charAt(i); 
            if (!current.containChild(c)) return false;
            current = current.getChild(c);
        }
        return current.isTerminated();
    }
    
    public boolean startsWith(String prefix) {
        Node current = this.rootNode;
        for (int i = 0, n = prefix.length() ; i < n ; i++) { 
            char c = prefix.charAt(i);
            if (!current.containChild(c)) return false;
            current = current.getChild(c);
        }
        return true;
    }
}
```

##### Trade-offs
![[Pasted image 20220701161634.png]]