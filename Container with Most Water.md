---
tags: LeetCode
topics: two pointers
difficulty: medium
performance: complete
date: 2022-07-24 Sunday
---

### Questions

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return _the maximum amount of water a container can store_.

**Notice** that you may not slant the container.

**Example 1:**

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

**Input:** height = `[1,8,6,2,5,4,8,3,7]`
**Output:** 49
**Explanation:** The above vertical lines are represented by array `[1,8,6,2,5,4,8,3,7]`. In this case, the max area of water (blue section) the container can contain is 49.

### Solution

- [[Two Pointers]] 
- Start with 2 furthermost pointers, these pointers represent the area with the greatest width. 
- Move the pointer representing the shorter line closer to find a taller line to <mark style="background: #FFB86CA6;">maximize height at the expense of width</mark> 

```Java
class Solution {
    public int maxArea(int[] height) {
        int lo = 0;
        int hi = height.length - 1;
        int maxArea = 0;
        while (lo < hi) {
            int width = hi - lo;
            int minHeight = Math.min(height[lo], height[hi]);
            if (width * minHeight > maxArea) {
                maxArea = width * minHeight;
            }
            if (height[lo] <= height[hi]) {
                lo++;
            } else {
                hi--;
            }
        }
        return maxArea;
    }
}
```
+ Proof: If we move the longer line, we _cannot_ increase the height for the simple reason that we are always limited by the shortest line, and we would be decreasing j-i, the width as well.
+ Time: O(n), Space: O(1)