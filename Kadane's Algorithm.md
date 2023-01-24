2022-06-05 16:13
Tags: [[Data Structure and Algorithm]] - [[Dynamic Programming]]  
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

## Main Points
An efficient solution to [[Maximum Sum Subarray]] problem. Find the contiguous subsequence such that the sum is maximum.

``` Python
def max_subarray(numbers):
    """Find the largest sum of any contiguous subarray."""
    best_sum = 0
    current_sum = 0
    for x in numbers:
        current_sum = max(0, current_sum + x) # if sum is ever negative, restart
        best_sum = max(best_sum, current_sum)
    return best_sum
```