---
layout: post
title: LeetCode | Max Points on a Line in Python
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
    Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.

Algorithm:
    1. use ax + by + c = 0 to avoid numerical problems.
    2. deal with coincidence of input points
'''


class Solution:
    # @param points, a list of Points
    # @return an integer
    def maxPoints(self, points):
        points = [(p.x, p.y) for p in points]
        points_set = list(set(points))
        cov = dict(zip(points_set, [0 for i in xrange(len(points_set))]))
        for j in xrange(len(points)):
            cov[points[j]] += 1
        if len(points_set) <= 2:
            return sum([cov[p] for p in points_set])
        max_global, l, dedup = 0, len(points_set), set()
        points = points_set
        for i in xrange(l):
            for j in xrange(i+1, l):
                if (i, j) in dedup:
                    continue
                a, b = points[j][1] - points[i][1], points[j][0] - points[i][0]
                c = points[i][1] * points[j][0] - points[j][1] * points[i][0]
                rec = [i, j]
                for k in xrange(j+1, l):
                    if points[k][0] * a - points[k][1] * b + c == 0:
                        rec.append(k)
                max_local = sum([cov[points_set[itr]] for itr in rec])
                for itr in xrange(len(rec)):
                    for itr2 in xrange(itr+1, len(rec)):
                        dedup.add((rec[itr], rec[itr2]))
                max_global = max(max_global, max_local)
        return max_global
</pre>
