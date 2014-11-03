---
layout: post
title: LeetCode | N-Queens in Python
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
    The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other. Given an integer n, return all distinct solutions to the n-queens puzzle. Each solution contains a distinct board configuration of the n-queens\' placement, where "Q" and "." both indicate a queen and an empty space respectively.

Algorithm:
    DFS
    use "occ" to store which columns has benn occupied
'''


class Solution:
    # @return a list of lists of string
    def solveNQueens(self, n):
        # DFS
        res = []
        board = [['.' for itr in xrange(n)] for itr1 in xrange(n)]
        occ = [1 << 31 for itr in xrange(n)]
        self.solveQueens_rec(n, 0, board, occ, res)
        return res

    def solveQueens_rec(self, n, level, board, occ, res):
        if level == n:
            res.append([''.join(itr) for itr in board])
        else:
            for i in xrange(n):
                if self.safe(level, i, occ):
                    occ[level] = i
                    board[level][i] = 'Q'
                    self.solveQueens_rec(n, level+1, board, occ, res)
                    board[level][i] = '.'
                    occ[level] = 1 << 31

    def safe(self, r, c, occ):
        for i in xrange(r+1):
            if occ[i] == c or occ[i]+i == r+c or occ[i] - i == c - r:
                return False
        return True
</pre>
