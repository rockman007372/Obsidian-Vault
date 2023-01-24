2022-07-04 17:03
Tags: [[LeetCode]] - [[Adddition Using Bit Manipulation]] - [[Binary Number]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Add Binary
### My Performance
#uncomplete #notOnTime #notOptimal 

### Questions
Difficulty: #easy??
Input: 2 string representing 2 binary numbers
Output: a string representing the binary sum

### Solution

##### Naive - O(M + N)
```Java
class Solution {
    public String addBinary(String a, String b) {
        // idea 1: O(M + N) transform back and forth
        return toBinary(toInteger(a));
        
    }
    
    public int toInteger(String binary) {
        int res = 0;
        for (int n = binary.length(), i = n - 1; i >= 0; i--) {
            char curr = binary.charAt(i);
            if (curr == '1') {
                res += Math.pow(2, n - i - 1);
            }
        }
        return res;
    }
    
    public String toBinary(int binary) {
        StringBuilder sb = new StringBuilder();
        if (binary == 0) return "0";
        while (binary != 0) {
            int digit = binary % 2;
            sb.append(digit);
            binary = binary / 2;
        }
        return sb.reverse().toString();
    }
}
```

##### Bit-by-Bit Manipulation - O(Max(M, N))
Basically basic addition but for base-2 (binary number) using a carry:
1001 + 1100 = 10101

- Time: O(max(M, N))
- Space: O(max(M, N) to keep the number, M and N are the size of the binary numbers!

```Java
class Solution {
    public String addBinary(String a, String b) {
        int n = a.length() - 1; int m = b.length() - 1;
        StringBuilder sb = new StringBuilder();
        int carry = 0;
        int total = 0;
        int i = 0, j = 0;
        
        // we add the binary numbers bit by bit.
        while (i <= n || j <= m) {
            int first = i <= n 
	            ? Character.getNumericValue(a.charAt(n - i)) 
	            : 0;
            int second = j <= m 
	            ? Character.getNumericValue(b.charAt(m - i)) 
	            : 0;
            total = first + second + carry; 
            
            // we add the summed digit to the result binary
            sb.append(total % 2 == 1 ? '1' : '0');
            // calculate the next carry
            carry = total / 2;
            // move to the next digits
            i++; j++;
        }
        
        if (carry != 0) {
            sb.append('1');
        }
        
        return sb.reverse().toString();
    }
}
```

##### Bit Manipulation - O(M + N)
- XOR operator gives the sum of 2 binary number *without* taking into account the carry.
- & operator gives the position of the carry
- <<1 gives the correct position of the carry
Time: O(M + N)
Space: O(Max(M, N)) - to store the result 

```Java
import java.math.BigInteger;
class Solution {
  public String addBinary(String a, String b) {
    BigInteger x = new BigInteger(a, 2);
    BigInteger y = new BigInteger(b, 2);
    BigInteger zero = new BigInteger("0", 2);
    BigInteger carry, answer;
    while (y.compareTo(zero) != 0) {
      answer = x.xor(y);
      carry = x.and(y).shiftLeft(1);
      x = answer;
      y = carry;
    }
    return x.toString(2);
  }
}
```
