---
tags: toProcess
course: CS2109S
type: guide
date: 2022-11-20 Sunday
---

## Graph question

Data structure for **queue** and **stacks**:
- List 
- collections.deque (preferred due to O(1) time complexity)

```python
# Queue using List
queue = []

queue.append(1)
queue.append(2)
queue.pop(0) # pop first element from queue, in this case, 1

# Stack using List
stack = []

stack.append('a')
stack.pop() # pop last element in stack


# Queue using collections.deque
from collections import deque

q = deque()
q.append('a')
q.popleft() # return 'a'

# Stack using collections.deque
stack = deque()
stack.append('a')
stack.pop()
```

Data structure for **Cache**: 
- Dictionary
- Set

```python

cache = set()
cache.add('a') # Will not add duplicates
'a' in cache # return true
cache.remove('a')


hash_table = {}
hash_table['even'] = 9
hash_table['odd'] = 10  # hash_table = {'even' : 9, odd' : 10}
hash_table['odd']       # return 10

```


## ML

##### Dataframe

```python
count_row = df.shape[0]  # Gives number of rows
count_col = df.shape[1]  # Gives number of columns

# obtain only no. rows
len(df.index) # fastest method


```

---
Links:
