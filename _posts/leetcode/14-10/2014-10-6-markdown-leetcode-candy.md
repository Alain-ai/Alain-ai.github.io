---
layout: post
title: LeetCode | Candy in Python
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
    There are N children standing in a line. Each child is assigned a rating value. You are giving candies to these children subjected to the following requirements:
    1. Each child must have at least one candy.
    2. Children with a higher rating get more candies than their neighbors.
    What is the minimum candies you must give?

Algorithm:
    two passes from two sides
'''


class Solution:
    # @param ratings, a list of integer
    # @return an integer
    def candy(self, ratings):
        res = [1]
        for i in xrange(1, len(ratings)):
            if ratings[i] > ratings[i-1]:
                res.append(res[i-1] + 1)
            else:
                res.append(1)
        for i in xrange(len(ratings)-2, -1, -1):
            if ratings[i] > ratings[i+1] and res[i] <= res[i+1]:
                res[i] = res[i+1] + 1
        return sum(res)
</pre>
