>[!problem]
> - A cache can store k items.
> - Sequence of m item request: $d_{1}, d_{2}, ..., d_{m}$
> - Cache hit: when item requested in alr in cache.
> - Cache miss: item not in cache and some item must be evicted and replaced by requested item (if cache is full).
> - ! Goal: Find an eviction schedule that minimize cache misses.

![[Pasted image 20230915110646.png]]

Notice we need some hindsight as to which item to evict. Imagine evicting item a, only to realise a will be requested right after. This leads us to a natural greedy solution:

>[!Farthest-in-Future]
> Whenever there is a cache miss, evict the item that will get requested the furthest in the future. 

While we cannot determine the future requests, we can *predict* it using some heuristics (**least-recently-used** algorithm). Hence Farthest-in-future is a guideline + benchmark for more practical algorithms.

## Proof

##### Definition

**Schedule** – A list that contains, for each, request, which item is brought into the cache, and which item is evicted

**Reduced Schedule** – a schedule that only brings in an item when there is a request for that item – so a non-reduced schedule would bring an item into the cache outside of a request for that item

##### Incentive

We have to prove:

>[!theorem]
> _Farthest-in-Future_ is the optimal algorithm that minimizes the number of cache misses.

Let SFF be our schedule given by our greedy algorithm. Let S be the the optimal schedule (that has a minimum number of cache misses). 

We can show that *it is possible to transform S into SFF* by performing a series of evictions without increasing the number of cache misses. Since S is already optimal, and the no. cache misses did not increase, SFF must be optimal as well.

The basis for the transformation is:

>[!theorem]
> Let S be a reduced schedule that is the same as SFF for the first j requests, then there is a reduced schedule S’ that is the same as SFF for the first j+1 requests, and incurs no more misses than S

We simply have to prove: After any request d, S = S' = SFF and the number of cache misses have not increased.

##### Proof

https://blog.henrypoon.com/blog/2014/02/02/proof-of-the-farthest-in-future-optimal-caching-algorithm/

