---
layout: post
title: LeetCode | Jump Game in Python
categories: LeetCode
tags: Python

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


<pre>
'''
Question:
    Given an array of non-negative integers, you are initially positioned at the first index of the array. Each element in the array represents your maximum jump length at that position. Your goal is to reach the last index in the minimum number of jumps.

    For example:
    Given array A = [2,3,1,1,4]

    The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

Algorithm:
    Greedy
'''


class Solution:
    # @param A, a list of integers
    # @return an integer
    def jump(self, arr):
        if len(arr) <= 1:
            return 0
        head = arr[0]
        i = 1
        cnt = 1
        while head < len(arr) - 1:
            cnt += 1
            max_head = 0
            while i <= head:
                max_head = max(max_head, arr[i] + i)
                i += 1
            i = head + 1
            head = max_head
        return cnt
</pre>
