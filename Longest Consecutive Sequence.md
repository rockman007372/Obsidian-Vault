2022-07-06 12:52
Tags: [[LeetCode]] - [[HashSet ]]- [[Union-Find]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Longest Consecutive Sequence
### My Performance
#uncomplete 

### Questions
Difficulty: #medium 
Input: unsorted integer array
Output: length of the longest consecutive sequence 

### Solution
##### HashSet with appropriate sequence building

Time: O(N)
-  Because the `while` loop is reached only when `curr` marks the beginning of a sequence (i.e. `curr-1` is not present in `nums`), the `while` loop can only run for n iterations throughout the entire runtime of the algorithm.
- Runtime of for-while loop = O(N + N)

Space: O(N)

```Java
class Solution {
    public int longestConsecutive(int[] nums) {        
        HashSet<Integer> map = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            map.add(nums[i]);
        }
        
        int longest = 0;
        int currentStreak = 0;
        
        for (int curr : nums) {
            // only consider nums that has no previous number.
            if (!map.contains(curr - 1)) {
                currentStreak = 0;
                int num = curr;
                
                while (map.contains(num)) {
                    currentStreak++;
                    num++;
                }
                
                longest = Math.max(longest, currentStreak);
            }
        }
        
        return longest;
    }
}
```

##### Union-Find

```Java
class UnionSet{
    int[] parents;
    int[] sizes;
    int[] ranks;
    UnionSet(int n){
        parents = new int[n];
        ranks = new int[n];
        sizes = new int[n];
        for(int i=0;i<n;i++){
            parents[i] = i;
        }
        Arrays.fill(sizes, 1);
    }
    
    public int union(int a, int b){
        // union by rank heuristic
        int idxA = findSet(a);
        int idxB = findSet(b);
		if(idxA == idxB)
		    return -1;
			
        if(ranks[idxA]>ranks[idxB]){
            parents[idxB] = idxA;
            sizes[idxA] += sizes[idxB];
            return sizes[idxA];
        } else {
            parents[idxA] = idxB;
            sizes[idxB] += sizes[idxA];
            if(ranks[idxB]==ranks[idxA]){
                ranks[idxB]++;
            }
            return sizes[idxB];
        }
    }
    
    public int findSet(int idx){
        // path compression heuristic
        if(parents[idx]!=idx)
            parents[idx] = findSet(parents[idx]);
        return parents[idx];
    }
}

class Solution {
    public int longestConsecutive(int[] nums) {
        int n = nums.length;
        if(n<=1){
            return n;
        }
        int longestConsecutiveSeqLen = 1;
		
        // to track index of each element in array
        Map<Integer, Integer> mp = new HashMap<>(); 
        UnionSet unionSet = new UnionSet(n);
        for(int i=0;i<n;i++){
            int e = nums[i];
            if(mp.containsKey(e)){
                continue;
            }
            mp.put(e, i);
            if (mp.containsKey(e-1)){
                longestConsecutiveSeqLen = Math.max(
	                longestConsecutiveSeqLen, 
	                unionSet.union(i, mp.get(e-1))
	            );
            }
            
            if (mp.containsKey(e+1)){
                longestConsecutiveSeqLen = Math.max(
	                longestConsecutiveSeqLen, 
	                unionSet.union(i, mp.get(e+1))
	            );
            }
            
        }
        return longestConsecutiveSeqLen;
    }
}
```