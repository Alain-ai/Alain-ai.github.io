---
layout: post
title: LeetCode | Longest Consecutive Sequence in Python
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
    Given an unsorted array of integers, find the length of the longest consecutive elements sequence. For example,
    Given [100, 4, 200, 1, 3, 2],
    The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4. Your algorithm should run in O(n) complexity.

Algorithm:
    1. put all elements into a set
    2. scan all elements
    3. for an element, search bidirectionally(incrementally and decrementally)
    4. when finding a new valid element, delete it from the set

Note:
    it would be less efficient if don\'t delete element and just use to dict to store a True value as visited
'''


class Solution:
    # @param num, a list of integer
    # @return an integer
    def longestConsecutive(self, num):
        # visited = dict(zip(num, [True for itr in xrange(len(num))]))
        visited = set(num)
        res = 0
        for i in num:
            # if visited.get(i, False):
            if i in visited:
                visited.remove(i)
                tmp_len, inc = 1, i + 1
                # while visited.get(inc, False):
                while inc in visited:
                    # visited[inc] = True
                    visited.remove(inc)
                    tmp_len, inc = tmp_len + 1, inc + 1
                inc = i - 1
                # while visited.get(inc, False):
                while inc in visited:
                    # visited[inc] = True
                    visited.remove(inc)
                    tmp_len, inc = tmp_len + 1, inc - 1
                res = max(res, tmp_len)
        return res
</pre>
