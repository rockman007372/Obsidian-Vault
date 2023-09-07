2022-06-05 16:13
Tags: [[Dynamic Programming]] - [[Data Structure and Algorithm]] - [[LeetCode]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

![[Pasted image 20220717093701.png||500]]
![[Pasted image 20220717093355.png||500]]
![[Pasted image 20220717093542.png||500]]

Time Complexity: O($N^2$) - N iteration, iteration i costs O(i).

## Solution

###  [[Dynamic Programming]] Solution

```Java
/*
Idea 1:
    1. State: DP[i] = length of LIS which ends at nums[i]
    2. Relation: DP[i] = Max(DP[j]) + 1 for 0 <= j < i and nums[j] < nums[i]
    3. Space = O(N)
    4. Time = O(N^2)
*/

class Solution {
    public int lengthOfLIS(int[] nums) {
        int len = nums.length;
        if (len == 0) return 0;
        
        int[] DP = new int[len];
        DP[0] = 1;
        int maxLIS = 1;
        for (int i = 1; i < len; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i] && DP[j] > DP[i]) {
                    DP[i] = DP[j];
                }
            }
            DP[i]++;
            
            if (maxLIS < DP[i]) maxLIS = DP[i];
        }
        
        return maxLIS;
    }
}
```

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [1 for i in range(n)]

        for index in range(n):
            for k in range(index):
                if nums[index] > nums[k]:
                    dp[index] = max(dp[index], dp[k] + 1)
        
        return max(dp)
```

###  [[Binary Search]] Solution

Let `S[i]` be defined as the smallest integer that ends an increasing sequence of length `i`. Now iterate through every integer `X` of the input set and do the following:

-   If `X` is more than the last element in `S`, then append `X` at the end of `S`. This essentially means we have found a new largest LIS.
-   Otherwise, find the smallest element in `S`, which is more than or equal to `X`, and replace it with `X`. Because `S` is sorted at any time, the element can be found using [binary search](https://www.techiedelight.com/binary-search/) in `log(N)` time.
-   In total, O(N x logN)

Illustration:

![[Pasted image 20230722022946.png]]

```
nums = [2, 6, 3, 4, 1, 2, 9, 5, 8]

Initialize to an empty set S = {}

Inserting 2 —- S = {2} – New largest LIS  
Inserting 6 —- S = {2, 6} – New largest LIS  
Inserting 3 —- S = {2, 3} – Replaced 6 with 3  
Inserting 4 —- S = {2, 3, 4} – New largest LIS  
Inserting 1 —- S = {1, 3, 4} – Replaced 2 with 1  
Inserting 2 —- S = {1, 2, 4} – Replaced 3 with 2  
Inserting 9 —- S = {1, 2, 4, 9} – New largest LIS  
Inserting 5 —- S = {1, 2, 4, 5} – Replaced 9 with 5  
Inserting 8 —- S = {1, 2, 4, 5, 8} – New largest LIS
```

```Java
/*
Idea 2: 
    1. State: DP[i] = SMALLEST element that is also the LAST ELEMENT in an LIS of length i
    2. DP is in increasing order as we build it -> Binary Search to update
    3. For each element in nums, we just have to update DP once! -> O(lgN) per iteration -> O(NlgN) in total
	eg: 
	1, 3, 4, 2, 1
	S = [1, 2, 4, INF, INF] -> max LIS = 3 
*/
class Solution {
    public int lengthOfLIS(int[] nums) {
        int len = nums.length;
        if (len == 0) return 0;
        
        // store smallest last element of LIS of length i + 1
        int[] S = new int[len];
        Arrays.fill(S, Integer.MAX_VALUE);
        S[0] = nums[0];
        int maxLIS = 0;
        
        for (int num : nums) {
	        // If num is more than the last element in `S`, then append num at the end of `S`
            if (num > S[maxLIS]) {
                maxLIS++;
                S[maxLIS] = num;
                continue;
            } 
	        
	        //  Otherwise, find the smallest element in `S`, which is more than or equal to num, 
	        // and replace it with num. 
            int idx = binarySearch(S, 0, maxLIS, num);
            S[idx] = num;
        }
        
        return maxLIS + 1;
    }
    
    private int binarySearch(int[] nums, int lo, int hi, int target) {
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] == target) return mid;
            if (nums[mid] > target) {
                hi = mid;
            } else {
                lo = mid + 1;
            }
        }
        return lo; // return the next smallest element's index
    }
}
```

Simplified Python solution:

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [float('inf') for i in range(n)]
        dp[0] = nums[0]

        for index in range(1, n):
            if nums[index] < dp[index - 1]:
                insertionPoint = bisect.bisect_left(dp, nums[index])
                dp[insertionPoint] = nums[index]
            
            elif nums[index] > dp[index - 1]:
                dp[index] = nums[index]

        return len(list(filter(lambda x : x != float('inf'), dp)))
```