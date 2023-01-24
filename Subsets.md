2022-07-14 16:04
Tags: [[LeetCode]] - [[Permutation]] - [[Backtracking]] - [[Dynamic Programming]] - [[Subsets II]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## My Performance
#complete 

## Questions
Difficulty: #medium
Input: `int[] nums`
Output: list of all the subsets of nums `int[][]`
Assumptions: All nums are unique, hence *there will not be duplicates*

## Solution
### Backtracking
```Java
// Idea
[]
[1]
[1, 2]
[1, 2, 3]
[1, 3] // backtrack
[2]
[2, 3]
[3]
```


```Java
class Solution {
    private List<List<Integer>> res;
    public List<List<Integer>> subsets(int[] nums) {
        res = new ArrayList<>();
        LinkedList<Integer> currList = new LinkedList<>();
        backtrack(currList, nums, 0);
        return res;
    }
    
    private void backtrack(LinkedList<Integer> curr, int[] nums, int idx) {
        res.add(new LinkedList<>(curr));
        for (int i = idx, n = nums.length; i < n; i++) {
            curr.add(nums[i]);
            backtrack(curr, nums, i + 1);
            curr.removeLast();
        }
    }
}
```

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:

        if not nums:
            return [[]]

        res = []

        def backtrack(idx: int, subset: List[int]):   
            res.append(list(subset)) # make a shallow copy of the subset
            for i in range(idx, len(nums)):
                subset.append(nums[i])
                backtrack(i + 1, subset)
                subset.pop()

        backtrack(idx=0, subset=[])
        return res
```


**Complexity Analysis** - quite similar to [[All Paths from Source to Target]]
- Time: O($N * 2^N$)
- Space: O(N)  
	- Recursion stack + space to hold current subset list 
	- If we also count the space to store result, then it will be `O(N * 2^N)` 


### Dynamic Programming
![[Pasted image 20220714165536.png]]

```Java
// A more intuitive solution
class Solution {
    private List<List<Integer>> res;
    public List<List<Integer>> subsets(int[] nums) {
        res = new ArrayList<>();
        res.add(new ArrayList<>());
        int subsetSize = 1;
        
        for (int num : nums) {
            for (int i = 0; i < subsetSize; i++) {
                ArrayList<Integer> subsetCopy = new ArrayList<>(res.get(i));
                subsetCopy.add(num);
                res.add(subsetCopy);
            }
            subsetSize = res.size();
        }
        return res;
    }
}
```

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:

        if not nums:
            return [[]]

        res = [[]]

        for i in range(len(nums)):
            element = nums[i]
            subsetWithElement = list(map(lambda subset : subset + [element], res))
            res += subsetWithElement

        return res
```


Even more elegant Python solution: 

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        output = [[]]
        
        for num in nums:
            output += [subset + [num] for subset in output]
        
        return output
```

- Time: O(N * $2^N$)
- Space: O(N) - O(N) space to create new copy of subset, which has max length of N

### Recursion - CS1101S

Basically the same idea as the DP solution, just iterative.

Time: `O(N * 2^N)` 
Space: `O(N * 2^N)` - $2^N$ subsets of at most N size?

```Java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        // change nums to linked list
        LinkedList<Integer> numsList = new LinkedList<>();
        for (int num : nums) {
            numsList.add(num);
        }
        
        return subsetHelper(numsList);
    }
    
    public List<List<Integer>> subsetHelper(LinkedList<Integer> xs) {
        // if xs is empty or null, return [[]]
        if (xs.size() == 0 || xs == null) {
            List<List<Integer>> res = new ArrayList<>();
            res.add(new ArrayList<>());
            return res;
        }
        
        // create all the subsets without head recursively
        Integer head = xs.removeFirst();
        List<List<Integer>> noHead = subsetHelper(xs);
        
        // create the subsets with head
        // by mapping the head to each subset without head
        List<List<Integer>> withHead = cloneList(noHead); // deep cloning
        for (List<Integer> subset : withHead) {
            subset.add(head);
        }
        
        // append the 2 sets together
        List<List<Integer>> append = new ArrayList<>();
        append.addAll(noHead);
        append.addAll(withHead);
        return append;
    }
    
    // create a deep copy of the list of lists
    private static List<List<Integer>> cloneList(List<List<Integer>> original) {
        List<List<Integer>> copy = new ArrayList<>(original.size());
        for (List<Integer> list : original) {
            copy.add(new ArrayList<>(list));
        }
        return copy;
    }
}
```

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:

        if not nums:
            return [[]]

        head = nums[0]

        subsetsWithoutHead = self.subsets(nums[1:])

        subsetsWithHead = list(map(lambda subset : [head] + subset,
							        subsetsWithoutHead))

        return subsetsWithoutHead + subsetsWithHead 
```