2022-06-05 16:44
Tags: [[LeetCode]] - [[Binary Tree]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Questions
Serialization is the process of **converting a data structure or object into a sequence of bits** so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. 

## Solution

Normally, we cannot do a single traversal, because it will not yield a unique tree. Hence a minimum of 2 traversals (Inorder + preorder/postorder) is required.

However, it turns out that if we include `#` or any other character for the `null` node while serializing, then **we can uniquely identify a tree**, that too with only one traversal (either preorder or postorder).


#### Iterative BFS - [[Breadth First Search]]
```Java
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();         
        
        // BFS using a QUEUE
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            TreeNode curr = queue.poll();
            if (curr == null) { 
                sb.append("null,");
            } else {
                sb.append(curr.val);
                sb.append(",");
                queue.add(curr.left);
                queue.add(curr.right);
            }
        }
        // return string
        return sb.toString();
    }
    
    // decode: 1,2,3,*,*,4,5,*,*,*,*, 
    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] code = data.split(",");
        
        // add root to queue
        if (code[0] == "null") return null;
        TreeNode root = new TreeNode(Integer.valueOf(code[0]));
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        // BFS to build tree and add next node
        int i = 0; int len = code.length;
        while (!queue.isEmpty() && i < len) {
            TreeNode curr = queue.poll();
            
            // add left tree
            i++;
            if (i < len) {
                String left = code[i];
                if (left.equals("null")) {
                    curr.left = null;
                } else {
                    curr.left = new TreeNode(Integer.valueOf(left));
                    queue.offer(curr.left);
                }    
            }
            
            // add right tree
            i++;
            if (i < len) {
                String right = code[i];
                if (right.equals("null")) {
                    curr.right = null;
                } else {
                    curr.right = new TreeNode(Integer.valueOf(right));
                    queue.offer(curr.right);
                }
            }
        }                                       
        return root;                                
    }
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));
```

Time: O(N) - go through all the nodes to serialize and deserialize.
Space: O(N) - Queue to store the nodes, max size = O(N)

#### Recursive DFS - preorder [[Depth First Search]]
The `DFS` strategy is more adapted for our needs, since the linkage among the adjacent nodes is naturally encoded in the order, which is rather helpful for the later task of `deserialization`.

```Java
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        preorderDFS(root, sb);
        return sb.toString();
    }
    
    public void preorderDFS(TreeNode root, StringBuilder sb) {
        if (root == null) {
            sb.append("null,");
        } else { 
            // root, left, right
            sb.append(root.val + ",");
            preorderDFS(root.left, sb);
            preorderDFS(root.right, sb);
        }
    }
    
    // decode: 1,2,null,null,3,4,null,null,5,null,null, 
    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] code = data.split(",");
        if (code[0].equals("null")) return null;
        TreeNode root = new TreeNode(Integer.valueOf(code[0]));
        int[] index = new int[]{0};
        return rhelper(root, code, index);
    }
    
    // instead of having an index to pass around, we can 
    // use a linked list and removeHead as we traverse
    public TreeNode rhelper(TreeNode root, String[] code, int[] index) {
        if (index[0] >= code.length) return null;
        if (code[index[0]].equals("null")) {
            index[0]++;
            return null;
        }
        root.val = Integer.valueOf(code[index[0]++]);
        root.left = rhelper(new TreeNode(), code, index);
        root.right = rhelper(new TreeNode(), code, index);
        return root;
    }   
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));

```