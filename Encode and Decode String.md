2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Encode and Decode String
### My Performance
#uncomplete

### Questions
Input: String
Expectation: Encode and decode

### Solution
See also: [[Serialize and Deserialize Binary Tree]]
##### Naive
```Java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        StringBuilder sb = new StringBuilder();
        String delimiter = Character.toString((char) 257);
        for (String s : strs) {
            sb.append(s);
            sb.append(delimiter);
        }
        sb.deleteCharAt(sb.length() - 1);
        return sb.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        String delimiter = Character.toString((char) 257);   
        String[] code = s.split(delimiter, -1);
        return Arrays.asList(code);
    }
}
```
Time: O(N)
Space: O(N) to store String array

##### Chunked Transfer Encoding
![[Pasted image 20220701004936.png]]
