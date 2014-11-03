---
layout: post
title: LeetCode | Best Time to Buy and Sell Stock in Python
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
    Say you have an array for which the ith element is the price of a given stock on day i. If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Algorithm:
    Greedy
    find the max profit at the ith day when we indeed sell the stock by storing the minimal prices(purchasing) at the days before the ith day
'''


class Solution:
    # @param prices, a list of integer
    # @return an integer
    def maxProfit(self, prices):
        if not prices:
            return 0
        res, min_cur = 0, prices[0]
        for i in xrange(1, len(prices)):
            res = max(res, prices[i] - min_cur)
            min_cur = min(min_cur, prices[i])
        return res
</pre>
