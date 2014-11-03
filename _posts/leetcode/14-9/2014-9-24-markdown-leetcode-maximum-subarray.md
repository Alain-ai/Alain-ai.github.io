---
layout: post
title: LeetCode | Maximum Subarray in Python
categories: LeetCode
tags: Python

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
jax: ["input/TeX","output/HTML-CSS"],
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]},
extensions: ["tex2jax.js","MathMenu.js","MathZoom.js"],
TeX: { equationNumbers: { autoNumber: "AMS" }, extensions: ["AMSmath.js", "AMSsymbols.js","noErrors.js","noUndefined.js"]}
});
</script>

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
</script>

<pre>
'''
Question:
    Find the contiguous subarray within an array (containing at least one number) which has the largest sum. For example, given the array [−2,1,−3,4,−1,2,1,−5,4], the contiguous subarray [4,−1,2,1] has the largest sum = 6. Try divide and conquer approach.

Note:
    divide and conquer temporarily not accepted

Algorithm:
    1. divide and conquer, for each execution, get the following three results
        1. maximum subarray result exactly starting from the 1st element
        2. maximum subarray result exactly ending up with the last element
        3. maximum subarray result can start or end anywhere
    2. DP
        to see whether DP[i-1] will contribute, DP[i] = max(DP[i-1] + A[i], A[i])
'''


class Solution:
    # @param A, a list of integers
    # @return an integer
    def maxSubArray(self, A):
        return self.maxSubArray_rec(A, 0, len(A) - 1)[2]

    def maxSubArray_rec(self, A, start, end):
        if end == start:
            return [A[start]] * 3
        mid = (start + end) >> 1
        max_left_left, max_left_right, res_left = self.maxSubArray_rec(A, start, mid)
        max_right_left, max_right_right, res_right = self.maxSubArray_rec(A, mid+1, end)
        res_local = max(max_left_right+max_right_left, res_left, res_right)
        max_left, cum_left = A[0], [A[0]]
        for i in xrange(start, end+1):
            cum_left.append(cum_left[-1] + A[i])
            max_left = max(max_left, cum_left[-1])
        max_right, cum_right = A[-1], [A[-1]]
        for i in xrange(end-2, start-1, -1):
            cum_right.append(cum_right[-1] + A[i])
            max_right = max(max_right, cum_right[-1])
        return max_left, max_right, res_local

    # @param A, a list of integers
    # @return an integer
    def maxSubArray(self, A):
        DP = [A[0]]
        for i in xrange(1, len(A)):
            DP.append(max(DP[-1] + A[i], A[i]))
        return max(DP)
</pre>
