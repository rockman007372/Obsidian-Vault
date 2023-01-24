2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Majority Element
### Questions
Input: Nums array
Output: Return the majority element (occuring at least $\lfloor \frac{n}{2} \rfloor$ times).

### Solution
#### Boyer-Moore Majority Voting Algorithm
Intuition: 
- The majority elements always occur more than the minority element. 
- If we divide the array into smaller suffixes, we can determine the majority element in each suffix?
  
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