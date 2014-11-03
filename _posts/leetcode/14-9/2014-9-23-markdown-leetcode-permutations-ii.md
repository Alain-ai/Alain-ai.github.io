---
layout: post
title: LeetCode | Permutations II in Python
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
Question: Given a collection of numbers that might contain duplicates, return all possible unique permutations. For example, [1,1,2] have the following unique permutations: [1,1,2], [1,2,1], and [2,1,1].

Algorithm: DFS, deduplicate when num[i] == num[i+1] after one execution
'''


class Solution:
    # @param num, a list of integer
    # @return a list of lists of integers
    def permuteUnique(self, num):
        num.sort()
        res = []
        visited = [False for itr in xrange(len(num))]
        self.permuteUnique_rec(num, 0, visited, [], res)
        return res

    def permuteUnique_rec(self, num, level, visited, stk, res):
        if level == len(num):
            res.append(stk)
        else:
            i = 0
            while i < len(num):
                if not visited[i]:
                    visited[i] = True
                    self.permuteUnique_rec(num, level+1, visited, stk+[num[i]], res)
                    visited[i] = False
                    while i < len(num) - 1 and num[i] == num[i+1]:
                        i += 1
                i += 1
</pre>
