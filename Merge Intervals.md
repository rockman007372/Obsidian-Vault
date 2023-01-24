2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Question
Input:  an array of intervals
Output: an array of intervals in which overlapping intervals are merged

### Solution
Method 1: 
+ Sort by lower bounds, then merge using lo and hi indices / simply merge
+ Time: O(nlgn + n) = O(nlgn)
+ Space: O(n) or O(lgn) due to sorting
+ See also: [[Sorting Algorithms]]

``` Java
// my solution
class Solution {
    public int[][] merge(int[][] intervals) {
        Comparator<int[]> comp = new Comparator<>() {
            public int compare(int[] first, int[] second) {
                return first[0] - second[0];
            }   
        };
        Arrays.sort(intervals, comp);
        
        int lo = intervals[0][0];
        int hi = intervals[0][1];
        List<int[]> res = new ArrayList<int[]>();
        for (int i = 0; i < intervals.length; i++) {
            if (i == intervals.length - 1) {
                res.add(new int[] {lo, hi});
                break;
            }
            
            if (hi < intervals[i + 1][0]) {
                int[] pair = new int[] {lo, hi};
                res.add(pair);
                lo = intervals[i + 1][0];
                hi = intervals[i + 1][1];
            } else {
                hi = Math.max(hi, intervals[i + 1][1]);
            }
        }
        
        int[][] result = new int[res.size()][];
        for (int i = 0; i < res.size(); i++) {
            result[i] = res.get(i);
        }
        return result;
    }
}

// More space efficient solution:
class Solution {
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

Method 2:
+ build graph
+ O(V + E) = O(n^2) ? 
