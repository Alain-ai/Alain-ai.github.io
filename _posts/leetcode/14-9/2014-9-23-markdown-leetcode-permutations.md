---
layout: post
title: LeetCode | Permutations in Python
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
Question: Given a collection of numbers, return all possible permutations. For example, [1,2,3] have the following permutations: [1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], and [3,2,1].

Algorithm: DFS
'''


class Solution:
    # @param num, a list of integer
    # @return a list of lists of integers
    def permute(self, num):
        num.sort()
        num.reverse()
        res = []
        visited = [False for itr in xrange(len(num))]
        self.permute_rec(num, 0, visited, [], res)
        return res

    def permute_rec(self, num, level, visited, stk, res):
        if level == len(num):
            res.append(stk)
        for i in xrange(len(num)):
            if not visited[i]:
                visited[i] = True
                self.permute_rec(num, level+1, visited, stk+[num[i]], res)
                visited[i] = False


    def permute(self, num):
        num.reverse()
        return [item for item in self.permute_rec(num)]

    def permute_rec(self, num):
        if len(num) == 1:
            yield num
        else:
            n = [num.pop()]
            for p in self.permute_rec(num):
                for i in xrange(len(p) + 1):
                    yield p[:i] + n + p[i:]
</pre>
