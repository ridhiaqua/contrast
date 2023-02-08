---
title: "Leetcode Problem #1425. Constrained Subsequence Sum"
layout: post
---

Given an integer array `nums` and an integer `k`, return the maximum sum of a non-empty subsequence of that array such that for every two consecutive integers in the subsequence, `nums[i]` and `nums[j]`, where `i < j`, the condition `j - i <= k` is satisfied.

A subsequence of an array is obtained by deleting some number of elements (can be zero) from the array, leaving the remaining elements in their original order.

 

Example 1:

```
Input: nums = [10,2,-10,5,20], k = 2
Output: 37
Explanation: The subsequence is [10, 2, 5, 20].
```
Example 2:
```
Input: nums = [-1,-2,-3], k = 1
Output: -1
Explanation: The subsequence must be non-empty, so we choose the largest number.
```
Example 3:
```
Input: nums = [10,-2,-10,-5,20], k = 2
Output: 23
Explanation: The subsequence is [10, -2, -5, 20].
```

Constraints:

- `1 <= k <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

My JavaScript solution :

```js
//have a window array that should not exceed the size k
//store index and lastKsum in that window array, initialize "max" to nums[0] 
//for nums length iterate over array, extract first elememt of window (index, lastKsum)
//check if window is in bound of k size.
//if not shift the first element out
//calculate the newsum which would be lastKsum/0 + nums[i]
//calcute max from max and newsum
//pop out the elements from window till their lastKsum is less than new sum or the window is empty
//push the index and new sum to window
//return max

var constrainedSubsetSum = function(nums, k) {
    var window = [[0,nums[0]]];
    var max = nums[0];
    for(var i=1; i<nums.length; i++){
        var [index,lastKsum] = window[0];
        if(index == i-k){
            window.shift();
        }
        var sum = Math.max(lastKsum, 0) + nums[i]
        max = Math.max(max, sum);
        while(window.length>0 && window[window.length-1][1] < sum){
            window.pop();
        }
        window.push([i,sum]);
    }
    return max;
};
```


