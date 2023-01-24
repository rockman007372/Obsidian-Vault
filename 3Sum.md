---
tags: LeetCode
topics: two pointers
difficulty: medium
performance: uncomplete
date: 2022-07-24 Sunday
---

### Questions

Input:
Output: 

### Solution

##### **Sort, then use triple indices:**  
+ Time: O(n^2)
+ Space: dependent on implementation of sorting algo, usually O(lgN) or O(n)![[Pasted image 20220604190237.png]]

```Java 
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        int lo, hi, sum;
        for (int i = 0; i < nums.length - 2 && nums[i] <= 0; i++) {
            if (i != 0 && nums[i] == nums[i - 1] ) {
                continue;
            }
            lo = i + 1;
            hi = nums.length - 1;
            while (lo < hi) {
                sum = nums[i] + nums[lo] + nums[hi];
                if (sum < 0) {
                    lo++;
                } else if (sum > 0) {
                    hi--;
                } else {
                    res.add(Arrays.asList(nums[i], nums[lo], nums[hi]));
                    lo++;
                    while (nums[lo] == nums[lo - 1] && lo < hi) {
                        lo++;
                    }   
                }
            }
        }
        return res;
    }
}
```

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        sorted_nums = sorted(nums)
        n = len(sorted_nums)
        res = []

        for x in range(n - 2):
            target = -1 * sorted_nums[x]
            
            if target < 0: # only iterate through the negative portion
                break
                
            # no duplicated target
            if x != 0 and sorted_nums[x] == sorted_nums[x - 1]:
                continue 
            y = x + 1
            z = n - 1
            
            # 2Sum algo
            while y < z:
                twoSum = sorted_nums[y] + sorted_nums[z]
                if  twoSum == target:
                    res.append([-target, sorted_nums[y], sorted_nums[z]])
                    y += 1
                    z -= 1
                    
                    # Ensure no duplicate triplets:
                    while y < z and sorted_nums[y] == sorted_nums[y - 1]:
                       y += 1 
                       
                elif twoSum < target:
                    y += 1
                else: 
                    z -= 1

        return res
```

##### **Sort, then use HashMap instead of indices**
   + [[Two Sum & Contain Duplicate]]
   + Search for `complement = -nums[i] - nums[j]`
   + 2 pass search
   + Time: O(n^2)

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        for i in range(len(nums)):
            if nums[i] > 0:
                break
            if i == 0 or nums[i - 1] != nums[i]:
                self.twoSum(nums, i, res)
        return res

    def twoSum(self, nums: List[int], i: int, res: List[List[int]]):
        seen = set()
        j = i + 1
        while j < len(nums):
            complement = -nums[i] - nums[j]
            if complement in seen:
                res.append([nums[i], nums[j], complement])
                while j + 1 < len(nums) and nums[j] == nums[j + 1]:
                    j += 1
            seen.add(nums[j])
            j += 1
```


##### **No sorting, just hashMap:**
+ Rely on Set to remove duplicate!!
+ But there's a neat trick to reuse the same HashMap for all iteration! Assign the element to the current iteration: `map.put(nums[j], i)  `

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res, dups = set(), set()
        for i, val1 in enumerate(nums):
            seen = set()
            if val1 not in dups:
                dups.add(val1)
                for val2 in nums[i+1:]:
                    complement = -val1 - val2
                    if complement in seen:
                        res.add(tuple(sorted((val1, val2, complement))))
                    else:
                        seen.add(val2)
        return res
```