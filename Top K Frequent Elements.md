---
tags: LeetCode, leetcode
topics: 
difficulty: medium
performance: uncomplete
date: 2022-07-24 Sunday
---

## Questions

Input: Nums array
Output: Top K most frequent elements

## Solution

### Bucket Sort

Time: O(N + K) = O(N)
Space: O(N) ?

```Java
class Solution {
    // Idea: Bucket Sort
    public int[] topKFrequent(int[] nums, int k) {
        if (nums.length == k) return nums;
        
        // 1. Hash nums to frequecy
        HashMap<Integer, Integer> freqMap = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            freqMap.put(nums[i], freqMap.getOrDefault(nums[i], 0) + 1);
        }
        
        // 2. Put nums into bucket of linked list, highest frequecy in front
        ArrayList<LinkedList<Integer>> buckets = putInBuckets(freqMap, nums.length);
        
        // 3. Traverse linked list until we have the first k elements
        int[] result = new int[k]; int resIndex = 0;
        for (LinkedList<Integer> bucket : buckets) {            
            while (!bucket.isEmpty()) {
                result[resIndex++] = bucket.remove();
                if (resIndex == k) return result;
            }
        }
        return result;
    }
    
    public ArrayList<LinkedList<Integer>> putInBuckets(
	    HashMap<Integer, Integer> freqMap, int length) {
        
        ArrayList<LinkedList<Integer>> buckets = 
	        new ArrayList<LinkedList<Integer>>();     
        
        for (int i = 0; i < length; i++) {
	        buckets.add(i, new LinkedList());
	    }
        
        for (Map.Entry<Integer,Integer> entry : freqMap.entrySet()) {
            int num = entry.getKey();
            int freq = entry.getValue();
            int index = length - freq;
            buckets.get(index).add(num);
        }
        
        return buckets;
    }
}
```

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        n = len(nums)

        # create freq hash
        freq = defaultdict(lambda: 0)
        for num in nums:
            freq[num] += 1
        
        # bucket sort: 
        # idea: frequency <= n 
        buckets = [[] for _ in range(n + 1)]  
        for num in freq:
            index = freq[num]
            buckets[index].append(num)
        
        # get the first k elements
        res = []
        for bucket in reversed(buckets):
            for num in bucket:
                res.append(num)
                k -= 1
                if k == 0:
                    return res
        return res
```

### Heap 

1. First create frequency HashMap. O(N)
2. Then build a [[Heap]] of size k, ordered by frequency, using N elements.
   - Add the first k elements in O(k) time average.
   - Add the remaining elements while maintaining size K in O($(N - k) * logK$) time.
3. Return the heap as an output array. O($k*logk$) to extract min k times.

Time: O($N*lgk$) 
Space: O(N + k), N for hashmap and k for heap

```Java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        if (nums.length == k) return nums;
        
        // 1. Hash nums to frequecy
        HashMap<Integer, Integer> freqMap = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            freqMap.put(nums[i], freqMap.getOrDefault(nums[i], 0) + 1);
        }
        
        // 2. Add into MaxHeap of size k
        PriorityQueue<Integer> heap = new PriorityQueue<>(k, (x, y) -> freqMap.get(x) - freqMap.get(y));
        for (int num : freqMap.keySet()) {
            heap.add(num);
            if (heap.size() > k) heap.remove();
        }
        
        // 3. Return output array
        int[] res = new int[k];
        for (int i = 0; i < k; i++) {
            res[i] = heap.remove();
        }
        return res;
    }
}

```

### Quick Select

Algorithm:
1. Build HashMap frequency
2. Use [[Quick Select]] to select the N - K most frequent element. Since frequency may be duplicated, the Partition Algorithm must be able to deal with duplicates
3. Return the the last K elements to the right of the partition pivot.

```Java
class Solution {
	HashMap<Integer, Integer> frequencies;
    
    public int[] topKFrequent(int[] nums, int k) {
        if (nums.length == k) return nums;
        
        // 1. Hash nums to frequecy
        frequencies = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            frequencies.put(nums[i], frequencies.getOrDefault(nums[i], 0) + 1);
        }
        
        // 2. create array of unique elements
        int size = frequencies.size();
        int[] unique = new int[size];
        int uniqueIndex = 0;
        for (int num : frequencies.keySet()) {
            unique[uniqueIndex++] = num;
        }
        
        // 3. quickSelect nums for the k - n element orderd by frequecy
        quickSelect(unique, 0, size - 1, size - k);
        
        // 4. return elements between the (n - k + 1)th element and last element
        return Arrays.copyOfRange(unique, size - k, size);
    }
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
	// LOMUTO PARTITION SCHEME
    public int partition(int[] nums, int lo, int hi, int pIndex) {
        int pivotFrequency = frequencies.get(nums[pIndex]);
        // swap pivot to the end
        swap(nums, hi, pIndex);
        int storedIndex = lo;
        
        // move all less frequent elems to the left
        for (int i = lo; i < hi; i++) {
            if (frequencies.get(nums[i]) < pivotFrequency) {
                swap(nums, storedIndex, i);
                storedIndex++;
            }
        }
        
        // move pivot to correct position
        swap(nums, hi, storedIndex);
        return storedIndex;
    }
    
    public void quickSelect(int[] nums, int lo, int hi, int k) {
	    if (lo < hi) {
		    int pIndex = ThreadLocalRandom.current().nextInt(lo, hi + 1);
            // partition about pIndex
            int p = partition(nums, lo, hi, pIndex);
            if (p == k - 1) return;
            if (p > k - 1) quickSelect(nums, lo, p - 1, k);
            if (p < k - 1) quickSelect(nums, p + 1, hi, k);
		}
    }   
}        
```

Time: O(N) on average 
Space: O(N) for HashMap

