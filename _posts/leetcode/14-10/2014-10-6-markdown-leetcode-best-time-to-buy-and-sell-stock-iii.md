---
layout: post
title: LeetCode | Best Time to Buy and Sell Stock III in Python
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
    Say you have an array for which the ith element is the price of a given stock on day i. Design an algorithm to find the maximum profit. You may complete at most two transactions.

Algorithm:
    Greedy
    find the max profit at the ith day when we indeed sell the stock by storing the minimal price(purchasing) at the days before the ith day
    find the max profit at the ith day when we indeed buy the stok by storing the maximal price(selling) at the days behind the ith day
'''


class Solution:
    # @param prices, a list of integer
    # @return an integer
    def maxProfit(self, prices):
        if not prices:
            return 0
        min_arr = [0 for itr in xrange(len(prices))]
        max_arr = min_arr[:]
        min_cur, max_pro = prices[0], 0
        for i in xrange(1, len(prices)):
            max_pro = max(max_pro, prices[i] - min_cur)
            min_arr[i] = max_pro
            min_cur = min(min_cur, prices[i])
        max_pro, max_cur = 0, prices[-1]
        for i in xrange(len(prices)-2, -1, -1):
            max_pro = max(max_pro, max_cur - prices[i])
            max_arr[i] = max_pro
            max_cur = max(max_cur, prices[i])
        return max(map(lambda x, y: x+y, max_arr, min_arr))
</pre>
