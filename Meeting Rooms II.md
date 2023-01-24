2022-07-09 19:01
Tags: [[LeetCode]] - [[Priority Queue]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### My Performance
#uncomplete 

### Questions
Difficulty: #medium 
Input: `int[][]` meeting intervals 
Output: min number of rooms to hold the intervals

### Solution

##### 1. Priority Queue
Idea: 
- Sort the intervals by starting times in increasing order.
- We need to keep the ending-time of the ROOMS in PQ.
- When we have a new meeting interval, we check the *earliest* ending time of the available rooms in PQ using PQ.peek()
	- If room is still in use, we just add a new room by adding the new ending time to the PQ
	- If room is available, we extractMin and add the new ending time to simulate room being used

Time: O(NLogN) - sort, then potentially remove and add rooms to the PQ for every interval.
Space: O(N)

```Java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if (intervals.length == 0) {
            return 0;
        }
        
        PriorityQueue<Integer> room = new PriorityQueue<>();
        
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        
        room.add(intervals[0][1]);
        
        for (int i = 1; i < intervals.length; i++) {
            if (room.peek() <= intervals[i][0]) {
                room.poll();
            }
            
            room.add(intervals[i][1]);
        }
        
        return room.size();
    }
}
```

##### 2. Sort Both Starting and Ending time

![[Pasted image 20220709190936.png||700]]
![[Pasted image 20220709191002.png||700]]

We dont need to keep track of which ending times belong to which intervals! We just need to know if the current starting time is later than the current earliest ending time!

Time: O(NlgN)
Space: O(N)

```Java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        int len = intervals.length;
        if (len == 0) return 0;        
        int[] startingTimes = new int[len];
        int[] endingTimes = new int[len];
        
        for (int i = 0; i < intervals.length; i++) {
            startingTimes[i] = intervals[i][0];
            endingTimes[i] = intervals[i][1];
        }
        
        Arrays.sort(startingTimes);
        Arrays.sort(endingTimes);
        
        int count = 0;
        int i = 0, j = 0;
        while (i < len && j < len) {
            if (startingTimes[i] < endingTimes[j]) {
                count++;
            } else {
                j++;
            }
            i++;
        }
        
        return count;
    }
}
```
