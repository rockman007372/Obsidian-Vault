2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Questions
Input: String s
Output: Numbers of all palindromic substring

Palindrome is a string that reads the same forwards and backwards.

## Solution
### DP solution
Check [[Dynamic Programming]] for framework

Time: O(N^2) - Check all ${{n}\choose{2}} = \frac{n(n - 1)}{2}$ possible substrings 
Space: O(N^2) - [[Tabulation]]

Overlapping Substructure: start from single length string, all the way to n-length string. The n-string result is dependent on the (n-1)-string result.

```Java
class Solution {
    public int countSubstrings(String s) {
        int n = s.length(), ans = 0;

        if (n <= 0) 
            return 0;

        boolean[][] dp = new boolean[n][n];

        // Base case: single letter substrings
        for (int i = 0; i < n; ++i) {
            dp[i][i] = true;
            ans++;
        }

        // Base case: double letter substrings
        for (int i = 0; i < n - 1; ++i) {
            dp[i][i + 1] = (s.charAt(i) == s.charAt(i + 1));
            ans += (dp[i][i + 1] ? 1 : 0);
        }

        // All other cases: substrings of length 3 to n
        for (int len = 3; len <= n; ++len)
            for (int i = 0, j = i + len - 1; j < n; ++i, ++j) {
                dp[i][j] = (s.charAt(i) == s.charAt(j)) && dp[i + 1][j - 1]; 
                ans += (dp[i][j] ? 1 : 0);
            }

        return ans;
    }
}
```

### Expand Around Possible Center
Time: O(N^2)
Space: O(1)

Idea: 
Each substring is either odd or even.

First, check every single character center. For each center, expand string on both side to see if the first and last char are the same. (N centers)

Secondly, check every paired center in the same way. (N - 1 centers)

```Java
class Solution {
    public int countSubstrings(String s) {
        int ans = 0;

        for (int i = 0; i < s.length(); ++i) {
            // odd-length palindromes, single character center
            ans += countPalindromesAroundCenter(s, i, i);

            // even-length palindromes, paired center
            ans += countPalindromesAroundCenter(s, i, i + 1);
        }

        return ans;
    }

    private int countPalindromesAroundCenter(String ss, int lo, int hi) {
        int ans = 0;

        while (lo >= 0 && hi < ss.length()) {
            // the first and last characters don't match!
            if (ss.charAt(lo) != ss.charAt(hi))
                break;
                
            ans++; // found a palindrome
            
            // expand around the center
            lo--;
            hi++;
            
        }

        return ans;
    }
}
```