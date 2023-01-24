---
tags: LeetCode
topics: greedy
difficulty: medium
performance: uncomplete
date: 2023-01-08 Sunday
---

### Questions

There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return _the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return_ `-1`. If there exists a solution, it is **guaranteed** to be **unique**

**Example 1:**

**Input:** 
gas = `[1,2,3,4,5]`
cost = `[3,4,5,1,2]`

**Output:** 3
**Explanation:**
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.

### Solution

##### Naive O(N^2)

Start at every point and check if we can move in circle.

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        # Naive solution: Check every starting point - O(N^2)
        
        n = len(gas)
        for start in range(n):
             tank = gas[start] # check if we can start at a point
             tank -= cost[start]
             if tank < 0:
                 continue
             station = (start + 1) % n
             
             while station != start: 
                 tank += gas[station]
                 tank -= cost[station]
                 if tank < 0:
                     break
                 station = (start + 1) % n
             
             if station == start:    
	             return start # if we reach here, we alr found a solution
             
         return -1
```

##### Greedy O(N)

**Observation:**
- There is no solution if sum(gas) < sum(cost).
- We can only start at station $i^{th}$ if `gas[i] > cost[i]`

**Greedy Algorithm:** 
Keep track of a variable `total `, which is the total difference between gas and cost so far. If `total < 0` at any station i, we reset `total` to 0 and start at the next station i + 1. 

**Why this works:**
- If the total gas in the tank is ever negative at a specific station, we cannot start at any stations before that station as total tank will still be negative regardless. The only choice is to start at the next station.
- We dont have to check the 2nd trip from station 0 to station Ns (only from Ns to N). Can prove using contradiction and a bit of math. 


```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:

        # Greedy O(N)
        if sum(gas) - sum(cost) < 0:
            return -1

        total = 0
        station = 0

        for i in range(len(gas)):
            total += gas[i] - cost[i]
            
            if total < 0:
                total = 0
                station = i + 1

        return station
```