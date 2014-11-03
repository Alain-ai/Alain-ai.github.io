---
layout: post
title: LeetCode | Word Ladder in Python
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
    Given two words (start and end), and a dictionary, find the length of shortest transformation sequence from start to end, such that:

    Only one letter can be changed at a time
    Each intermediate word must exist in the dictionary

Algorithm:
    BFS
    To change a char in a string, it is much faster to use s_new = s[:i] + x(s[i]) + s[i+1:] than use
    1. arr = list(s)
    2. arr[i] = x
    3. s_new = "".join(arr)

Note:
    Return 0 if there is no such transformation sequence.
    All words have the same length.
    All words contain only lowercase alphabetic characters.
'''


class Solution:
    # @param start, a string
    # @param end, a string
    # @param dict, a set of string
    # @return an integer
    def ladderLength(self, start, end, dict_input):
        dict_input.add(end)
        alphabeta = [chr(ord('a') + itr) for itr in xrange(26)]
        q, level = collections.deque([start, None]), 0
        while q:
            node = q.popleft()
            if not node:
                if not q:
                    break
                level += 1
                q.append(None)
            else:
                if node == end:
                    return level+1
                for i in xrange(len(node)):
                    for a in alphabeta:
                        if node[i] != a:
                            word = node[:i] + a + node[i+1:]
                            if word in dict_input:
                                q.append(word)
                                dict_input.remove(word)
        return 0
</pre>
