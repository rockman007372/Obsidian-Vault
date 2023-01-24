2022-06-28 00:33
Tags: [[TIPS]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Question Types
### Main Points
#### 1. Arrays
- Subarray: A range of contiguous values within an array
- Subsequence: A subarray with some values removed (order intact)
	- Eg: `[1, 2, 3, 4, 5] -> [1, 3, 5]`

###### [[Prefix Sum]]
`PrefixSum[i]` = sum from index 0 to 1 
Subarray sum between index j and i = `prefixSum[j] - prefixSum[i - 1]` 

###### [[Sliding Window]]
Ensure each value is visited at most twice.

#### 2. String
Should know the language String operations complexities!

###### Anagram - [[Group Anagram]]
Words with the same letters rearranged.
Possible approach: All anagrams have the same sorted order.

###### Palindrome - [[Palindromic Substring]]
Words that read the same forwards and backwards.
Possible approach: take a middle char and expand

#### 3. Intervals - [[Merge Intervals]] 
Required to merge, insert, find intersect...
Possible approach: 
- Sort either low end or high end
- Use min and max cleverly

#### 4. Binary Search
Read [[Binary Search]] for more info.

#### 5. Tree
- Types of tree: Usually [[Binary Tree]]
- Traversals: 
	- 3 types of DFS
	- BFS

#### 6. Graph
- [[Depth First Search]] - both recursive and stack implementation
- [[Breadth First Search]] - use deque/ linked list
- [[Topological Sort]]
- [[SSSP]] ?
- [[Backtracking]]: Restore previous state of visited nodes after exploring current path (leaving and retrieving breadcrumbs).
