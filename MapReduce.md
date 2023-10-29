- commonly used in big data processing frameworks like [[Hadoop]]. 
- process and generate large datasets that can be distributed across a cluster of computers (distributed data processing.)


>[!Clarifications]
>- **Worker**: a physical machine.
>- **Split**: A smaller standard-sized chunk of the input data.
>- **Map task**: a job requiring to process one split.
>	- A single worker can handle multiple map tasks. Once it completes a map task (finished processing a split), it is reassigned to another map task.
>- **Mapper/Reducer**: the process executing a map/reduce task. 
>	- If there are 5 map tasks, we need 5 mappers, but maybe fewer workers (e.g. 3)
>- **Map function**: a single call to the user-defined map function.
>	- A single map task can involve many calls to map functions.


A MapReduce program consists of two main stages:

![[Pasted image 20230923110346.png]]

1. **Map Stage:** 
- The input data is divided into smaller chunks, called **splits**. Each split corresponds to 1 **map task**. Each **worker** can only execute one map task at a time.
- Each worker iterates throught the (key, value) pairs in its split, and apply the map function on each pair.
- The map function is typically designed to perform some filtering, sorting, or transformation of the data.
- ! Each worker writes the outputs of the map function to intermediate files on its own local disk (each worker is a pc). *These files are partitioned by key.* 
	- e.g. `key = a, value = (1, 2, 3, 4)`

2. **Reduce Stage:** 
- Each reduce worker is responsible for 1 or more keys. It reads the data from the **corresponding key partition** of each mapper's local disk.
- Each worker then applies the reduce function on each key.
- The reduce function's output is typically written to an external storage system or used for further analysis.

## Typical Interface

```python
# process each (key, value) pair
# return a list of processed (key, value) pairs
map(k1, v1) -> List(k2, v2)

# do computation on a list of values, grouped by their key
reduce(k2, List(v2)) -> List(k3, v3)
```

![[Pasted image 20230923104429.png]]
## Other steps to take note (in sequential order)

**Combiner step**: "mini-reducers", locally aggregate output from **mappers** => reduce disk write and disk reads between map and reduce stages.

![[Pasted image 20230923111043.png]]

- Combiner may or may not be called. It is called if the worker finishes its map task early => User's responsible for ensuring correctness.
- Reducer can be used as combiners when operation is both *associative* and *commutative*.
	- associative: a + (b + c) = (a + b) + c
	- commutative: a + b = b  + a

**Partition step**: decides which reducers take on which key. 
- By default, decided by a hash function. 
- User can implement custom partition to spread out load among reducers.

**Shuffle step**: ensure that all key-value pairs with the same key end up on the same reduce worker.
- Comprised of local write and remote read
- Happens partly on map workers (pc), and partly on reduce workers.

## Guidelines to design good MapReduce

1. Linear scalability: More nodes mean more works done (in linear time)
2. Minimize disk and network I/O.
3. ! Reduce memory working set of each worker (e.g. memory to store hashmap, ...)

#### Example

Compare these 3 versions of a program, which counts the number of distinct words in a text file.

Version 0: Process each word in the split one by one.

![[Pasted image 20230923111743.png]]

Version 1: Maintain a count for **each line** (tuple) in the split.

![[Pasted image 20230923111752.png]]

Version 2: Maintain a count over the **whole split**.

![[Pasted image 20230923111801.png]]

## Secondary Sort

**Problem:** A reducer processes a key, but the data from the same key arrive unsorted (Tuples having the same key but arrive out of order).

**Solution:** Define a composite key (K1, K2). K1 is the original key and K2 is the key to sort by.

**Example:** Assume we want to compute some statistics (median, 25% quantile, etc.) of the data grouped by month.

Initially, each temperature value arrives at each reducer unsorted. Sorting the temperature at each reducer is potentially costly.

![[Pasted image 20230923122237.png]]

Hence, we can **"borrow" the tuple distributing process to sort the values for us.** This requires a composite key. First key is for partitioning, second key is for sorting.

![[Pasted image 20230923112313.png]]

![[Pasted image 20230923122037.png]]