---
tags:
  - LeetCode
  - leetcode
topics: dp, greedy
difficulty: 
performance: 
date: 2022-07-24 Sunday
---
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Questions

Input: Array of intervals `int[][] intervals`
Output: Minimum numbers of intervals removed so that no intervals overlapped 

## Solution

### Dynamic Programming

Sort the intervals by lower bound.
State: DP[i] = max number of non-overlapping intervals from start to i
Relation: DP[i] = Max(DP[j]) + 1, where $0 \leq j < i$ , if there is no overlap between intervals[i] and intervals[j]
result = intervals.length - max number of non-overlapping intervals 

```Java
class Solution {
  class myComparator implements Comparator<int[]> {
    public int compare(int[] a, int[] b) {
      return a[1] - b[1];
    }
  }
  
  public boolean isOverlapping(int[] i, int[] j) {
    return i[1] > j[0];
  }
  
  public int eraseOverlapIntervals(int[][] intervals) {
    if (intervals.length == 0) {
      return 0;
    }
    Arrays.sort(intervals, new myComparator());
    int dp[] = new int[intervals.length];
    dp[0] = 1;
    int ans = 1;
    for (int i = 1; i < dp.length; i++) {
      int max = 0;
      for (int j = i - 1; j >= 0; j--) {
        if (!isOverlapping(intervals[j], intervals[i])) {
          max = Math.max(dp[j], max);
        }
      }
      dp[i] = max + 1;
      ans = Math.max(ans, dp[i]);
    }
    return intervals.length - ans;
  }
}
```

Time: O($N^2$) due to double for loop
Space: O(N) due to tabulation

### Greedy Algorithm where the lower bound is sorted

1. Sort by lower bound.
2. Traverse from left to right. There will be 3 cases:
   ![[Pasted image 20220622224732.png]]
   + Case 1: Continue
   + Case 2: Remove bigger interval (prior interval)
   + Case 3: Remove the latter interval

```Java
class Solution { 
    public int eraseOverlapIntervals(int[][] intervals) {
        // sort first
        Arrays.sort(intervals, (x,y) -> x[0] - y[0]);

        int len = intervals.length;
        int[] prev = intervals[0]; 
        int[] curr;
        int count = 0;
        for (int i = 1; i < len; i++) {
            curr = intervals[i];
            if (curr[0] < prev[1]) {
                if (curr[1] < prev[1]) {
                    prev = curr;
                }
                count++;
                continue;
            }
            prev = curr;
        }
        return count;
    }
}
```

Time: O(NlogN) due to sorting
Space: O(1)

### Greedy where upper bound is sorted

Instead of dividing into cases like above, we can sort the intervals by the upper bound first, then iterate **from left to right.**

Whenever there is overlap, we always **remove the latter interval** (current interval).

Why does this work?

![[Pasted image 20230905104422.png]]

```Java
class Solution {
  class myComparator implements Comparator<int[]> {
    public int compare(int[] a, int[] b) {
      return a[1] - b[1];
    }
  }

  public int eraseOverlapIntervals(int[][] intervals) {
    if (intervals.length == 0) {
      return 0;
    }
    Arrays.sort(intervals, new myComparator());
    int end = intervals[0][1];
    int count = 1;
    for (int i = 1; i < intervals.length; i++) {
      if (intervals[i][0] >= end) {
        end = intervals[i][1];
        count++;
      }
    }
    return intervals.length - count;
  }
}
```