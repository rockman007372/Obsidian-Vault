2022-07-06 13:44
Tags: [[LeetCode]] - [[Merge Intervals]] - [[Meeting Rooms II]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### My Performance
#complete #onTime 

### Questions
Difficulty: #easy
Find if there is overlappping intervals

### Solution

Basically just have to sort by lower bounds first.

```Java
class Solution {
    public boolean canAttendMeetings(int[][] intervals) {
        Arrays.sort(intervals, (x, y) -> x[0] - y[0]);
        int idx = 0, len = intervals.length;
        while (idx < len) {
            if (idx == 0 || intervals[idx - 1][1] <= intervals[idx][0]) {
                idx++;
            } else {
                return false;
            }
        }
        return true;
    }
}
```