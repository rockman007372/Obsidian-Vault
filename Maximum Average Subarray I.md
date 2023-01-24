2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Questions
Given a integer array `nums` and target `k`, return the max average contiguous subarray 

### Solution
- Make use of [[Sliding Window]] technique
- Finding max average is equivalent to finding max sum of contiguous subarray → [[Kadane's Algorithm]]

**MT1:**
2 pointer lo and hi at k space apart

**MT2:** 
At i, i > k iteration:
CurrentSum = currentSum - nums[i] + nums[i - k]; 

```Java 
public class Solution {
	public double findMaxAverage(int[] nums, int k) {
		int lo = 0;
		int hi = lo + k - 1; // watch off by 1 error
		double currentAve = 0;
		for (int i = 0; i < k; i++) {
			currentAve += nums[i];
		}
		double maxAve = currentAve;
		while (hi <= nums.length - 2) {
			currentAve = currentAve - nums[lo] + nums[hi + 1];
			hi++;	
		    lo++;
            maxAve = Math.max(currentAve, maxAve);
        }
		return maxAve / k;
	}
}

// alternatively
public class Solution {
    public double findMaxAverage(int[] nums, int k) {
        double sum=0;
        for(int i=0;i<k;i++)
            sum+=nums[i];
        double res=sum;
        for(int i=k;i<nums.length;i++){
            sum+=nums[i]-nums[i-k];
                res=Math.max(res,sum);
        }
        return res/k;
    }
}
```

