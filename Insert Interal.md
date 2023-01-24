2022-07-05 17:53
Tags: [[LeetCode]] - [[Merge Intervals]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Insert Interal
### My Performance

### Questions
Difficulty: #medium??
Input: `int[][]` intervals and a `int[]` newInterval
- intervals is sorted in increasing order by lower bounds, and there is no overlapping intervals.

Output: an `int[][]` intervals where the new interval is inserted and there is no overlapping intervals

### Solution
##### Binary Search then Merge
Most naive solution.

Time: O(logN + N + N) = O(N)
- [[Binary Search]] for position of new interval.
- Add new interval to new array
- Merge the array using helper function - O(N)

Space: O(N)

```Java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {        
        int len = intervals.length;
        if (len == 0) return new int[][]{newInterval};
        int pos = binarySearch(intervals, newInterval[0], 0, len - 1);
        
        int[][] insertedIntervals = new int[len + 1][];
        for (int i = 0, j = 0; i < len + 1; i++) {                 
            if (pos == -1) {
                insertedIntervals[i] = newInterval;
                pos--;
                continue;
            }
            
            insertedIntervals[i] = intervals[j++];
            // System.out.println("yeah");
            if (i == pos) {
                insertedIntervals[++i] = newInterval;
                // System.out.println("yeah");
            }
        }

        return merge(insertedIntervals);
    }
    
    // at the final position, if target >= element at final position, 
    // its insertion position there. Else, its at the left.
    public int binarySearch(int[][] intervals, int target, int lo, int hi) {
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            int midElem = intervals[mid][0];
            if (midElem == target) return mid;
            if (midElem > target) {
                hi = mid;
            } else if (midElem < target)  {
                lo = mid + 1;       
            }
        }
        return intervals[lo][0] > target 
            ? lo - 1 
            : lo;
    }

    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        LinkedList<int[]> merged = new LinkedList<>();
        for (int[] interval : intervals) {
            // if the list of merged intervals is empty or if the current
            // interval does not overlap with the previous, simply append it.
            if (merged.isEmpty() || merged.getLast()[1] < interval[0]) {
                merged.add(interval);
            }
            // otherwise, there is overlap, so we merge the current and previous
            // intervals.
            else {
                merged.getLast()[1] = Math.max(merged.getLast()[1], interval[1]);
            }
        }
        return merged.toArray(new int[merged.size()][]);
    }
}
```

##### More efficient solution without using Binary Search.

Make use of [[Merge Intervals]] ideas.

Algorithm: 
-   Add to the output all the intervals starting before `newInterval`.
-   Add to the output `newInterval`. Merge it with the last added interval if `newInterval` starts before the last added interval.
-   Add the next intervals one by one. Merge with the last added interval if the current interval starts before the last added interval.

Time: O(N)
Space: O(N)

My solution:
```Java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        // if intervals is empty, just add the newInterval
        if (intervals.length == 0) { 
            return new int[][] {newInterval};
        }
        
        LinkedList<int[]> merged = new LinkedList<>();
        boolean inserted = false;
        for (int[] interval : intervals) {
            // add newInterval right before the current interval
            if (inserted == false && newInterval[0] <= interval[0]) {
                if (merged.isEmpty() || merged.getLast()[1] < newInterval[0]) {
                    merged.add(newInterval);                                        
                } else {
                    merged.getLast()[1] = Math.max(merged.getLast()[1], newInterval[1]);
                }
                inserted = true;
            }
            
            // check if current interal overlaps with the previous interval
            if (merged.isEmpty() || merged.getLast()[1] < interval[0]) {
                merged.add(interval);
            } else {
                merged.getLast()[1] = Math.max(merged.getLast()[1], interval[1]);   
            }
        }
        
        // if we add new interval at the end
        if (merged.isEmpty() || merged.getLast()[1] < newInterval[0]) {
            merged.add(newInterval);                                        
        } else {
            merged.getLast()[1] = Math.max(merged.getLast()[1], newInterval[1]);
        }
        
        return merged.toArray(new int[merged.size()][]);
    }
}
```

Slightly better solution closer to algorithm:
```Java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        int len = intervals.length;
        // if intervals is empty, just add the newInterval
        if (len == 0) { 
            return new int[][] {newInterval};
        }
        
        LinkedList<int[]> merged = new LinkedList<>();
        int index = 0;
        
        // add all intervals before newInterval to merged list
        while (index < len && intervals[index][0] < newInterval[0]) {
            merged.add(intervals[index++]);
        }
        
        // insert new interval
        if (merged.isEmpty() || merged.getLast()[1] < newInterval[0]) {
            merged.add(newInterval);                                        
        } else {
            merged.getLast()[1] = Math.max(merged.getLast()[1], newInterval[1]);
        }
        
        // insert remaining intervals, making sure there is no overlap
        while (index < len) {
            if (merged.getLast()[1] < intervals[index][0]) {
                merged.add(intervals[index]);
                index++;
            } else {
                merged.getLast()[1] = Math.max(merged.getLast()[1], intervals[index++][1]);
            }
        }
        
        return merged.toArray(new int[merged.size()][]);
    }
}
```