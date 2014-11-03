---
layout: post
title: LeetCode | Longest Substring Without Repeating Characters in Python
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
    Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

Algorithm:
    1. store the index where a char shows up last time
    2. if there exists a repetition between "start" and current index i, "start" will be assigned to be the next one of the index where the repetition occurs
'''


class Solution:
    # @return an integer
    def lengthOfLongestSubstring(self, s):
        if not s:
            return 0
        flag = [-1 for i in xrange(256)]
        flag[ord(s[0])] = start = 0
        max_len = 1
        for i in xrange(1, len(s)):
            if flag[ord(s[i])] >= start:
                start = flag[ord(s[i])] + 1
            flag[ord(s[i])] = i
            max_len = max(max_len, i - start + 1)
        return max_len
</pre>
