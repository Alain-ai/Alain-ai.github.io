---
layout: post
title: LeetCode | Count and Say in Python
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
    The count-and-say sequence is the sequence of integers beginning as follows:

    1, 11, 21, 1211, 111221, ...
    1 is read off as "one 1" or 11.
    11 is read off as "two 1s" or 21.
    21 is read off as "one 2, then one 1" or 1211.
    Given an integer n, generate the nth sequence.

Note:
    The sequence of integers will be represented as a string.

Algorithm:
    straightforward
'''


class Solution:
    # @return a string
    def countAndSay(self, n):
        # corner case: n == 1
        if n == 1:
            return '1'
        res = [1]
        for i in xrange(1, n):
            cnt, num = 1, res[0]
            tmp = []
            for j in xrange(1, len(res)):
                if res[j] == res[j-1]:
                    cnt += 1
                else:
                    tmp += [cnt, num]
                    cnt, num = 1, res[j]
            tmp += [cnt, num]
            res = tmp
        return ''.join([str(itr) for itr in res])
</pre>
