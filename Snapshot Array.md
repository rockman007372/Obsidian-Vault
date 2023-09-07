---
tags: LeetCode, leetcode
topics: binarySearch
difficulty: medium
performance: uncomplete
date: 2023-06-14 Wednesday
---

## Questions

Implement a SnapshotArray that supports the following interface:

- `SnapshotArray(int length)` initializes an array-like data structure with the given length. **Initially, each element equals 0**.
- `void set(index, val)` sets the element at the given `index` to be equal to `val`.
- `int snap()` takes a snapshot of the array and returns the `snap_id`: the total number of times we called `snap()` minus `1`.
- `int get(index, snap_id)` returns the value at the given `index`, at the time we took the snapshot with the given `snap_id`

## Solution

### Binary search 

Idea: 
- Keep a series of snapshot (list / dict) for each element. Only update individual element snapshot at each `snap` instead of updating every single element
- For a `get` operation, use [[Binary Search]] to find the **rightmost** snap_id at the requested id.
- Notice the behaviour of `bisect_right`: it returns the index of the smallest element greater than target.

```python
class SnapshotArray:
    def __init__(self, length: int):
        self.currentArray = [[(-1, 0)] for _ in range(length)]
        self.currentId = 0
        
    def set(self, index: int, val: int) -> None:
        self.currentArray[index].append((self.currentId, val))

    def snap(self) -> int:
        self.currentId += 1
        return self.currentId - 1
        
    def get(self, index: int, snap_id: int) -> int:
        snapshots = self.currentArray[index]

        #  binary search to find the latest snap before snap_id (inclusive)
        snapRange = [i for (i, _) in snapshots]
        idx = bisect.bisect_right(snapRange, snap_id) - 1

        return snapshots[idx][1]

# Your SnapshotArray object will be instantiated and called as such:
# obj = SnapshotArray(length)
# obj.set(index,val)
# param_2 = obj.snap()
# param_3 = obj.get(index,snap_id)
```

Let N be the total number of function calls and k be the length of the array.

Time: 
- constructor: O(k)
- snap: O(1)
- get: O(lgN) for each operation
- set: O(1)

Space: O(N + k)

---
Link: [[LeetCode]]
