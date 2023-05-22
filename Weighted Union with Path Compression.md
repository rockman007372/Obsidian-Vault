
Almost constant time for both Find and Union

Final amortized time complexity is `O(α(n))`, where α(n) is the inverse Ackermann function, which grows very slowly.

Worst case run time is still O(lgN), but if we call m such calls consecutively, amortized run time is O(α(n)).

![[Pasted image 20220616150324.png]]