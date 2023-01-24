2022-06-05 16:14
Tags: [[Data Structure and Algorithm]]  
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Main Points
+ From array A, create a prefix sum array P where `P[j] = A[0] + A[1] + ... + A[j]`
+ `PrefixSum[i]` = sum from index 0 to 1 
+ Subarray sum between index j and i = `prefixSum[j] - prefixSum[i - 1]`
  
   ![[PrefixSum Illustration.png]]