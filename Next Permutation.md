2022-06-05 16:44
Tags: [[LeetCode]] - [[Permutation (Leet)]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Next Permutation
### My Performance

### Questions
Input: nums int array
Output: next (larger) permutation of the number.

### Solution
##### One pass greedy
Idea: 
- For non-increasing array: `[3, 2, 1]`, there is no next bigger permutation, hence we just reverse the whole array.
- Otherwise, we find the first pivot point `a[i]` where `a[i] < a[i + 1]`, such as point `4` in `[4,5,3,1]`
- Since everything on the right side of `4` is non-increasing, we cannot permute the right side in anyway.
- We just swap `4` with the first larger element going from the right , `5`. Now we have `[5, 4, 3, 1]`.
- Now we just need to the reverse the right portion `[4, 3, 1]` to get the next permutation

![[Pasted image 20220702112003.png]]

Time: O(N)
Space: O(1)

```Java
class Solution {
    public void nextPermutation(int[] nums) {
        int len = nums.length;
        int left = len - 2;
        while (left >= 0 && nums[left] >= nums[left + 1]) {
            left--;
        }
        
        if (left == -1) {
            reverse(nums, left + 1);
            return;
        }
        
        int right = len - 1;
        while (right > left && nums[right] <= nums[left]) {
            right--;
        }
        swap(nums, left, right);
        reverse(nums, left + 1);
    }
    
    public void swap(int[] nums, int i, int j) {
        if (i == j) return;
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    public void reverse(int[] nums, int i) {
        for (int j = nums.length - 1; j > i; j--) {
            swap(nums, i, j);
            i++;
        }
    }
}
```