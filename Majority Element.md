---
tags:
  - LeetCode
  - leetcode
topics: divide-and-conquer, greedy
difficulty: hard
performance: uncomplete
date: 2022-07-24 Sunday
---
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Questions

Input: Nums array
Output: Return the majority element (occuring **more than** $\lfloor \frac{n}{2} \rfloor$ times).
Assumption: majority element always exists

## Solution
### Boyer-Moore Majority Voting Algorithm

Observation:
- If there is a majority element, it will cancel out non-majority elements when paired one-on-one in the voting process. Therefore, the majority element will eventually stand out.
  
```Java
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        Integer candidate = null;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
}
```

Time: O(N)
Space: O(1)

#### Proof

Assume the array of n elements has a majority element M. When we apply the algorithm on the array, either:

- Case 1: counter never drops to zero
- Case 2: counter drops to zero at some point x < n

In case 1, the output gives the correct majority element. Count is the **difference** between the number of majority elements and the number of non-majority element, which is always greater than 0.

In case 2, this means either the majority element does not exist in the range `[0, x]` or it exists but got outnumbered by non-majority elements.

If it does not exist in that range, it must still be the majority element in the remaining `[x, n]` range. Hence if we apply the algorithm on that range, counter will never be zero.

If it does exist but got outnumbered, the number of M in range `[0, x]` must be at most `x / 2`.  Since the total numbef of M must be at least `n / 2 + 1`, the remaining number of M in range `[x, n]` must be at least $$\frac{n}{2}+1- \frac{x}{2}=\frac{n-x}{2} + 1$$
Hence, M must still be the majority element of the remaining range, and therefore the algorithm will return the correct output.


