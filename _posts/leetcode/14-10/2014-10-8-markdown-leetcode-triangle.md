---
layout: post
title: LeetCode | Triangle in Python
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
    Write a program to solve a Sudoku puzzle by filling the empty cells. Empty cells are indicated by the character '.'. You may assume that there will be only one unique solution.

Algorithm:
    DFS
'''


class Solution:
    # @param board, a 9x9 2D array
    # Solve the Sudoku by modifying the input board in-place.
    # Do not return any value.
    def solveSudoku(self, board):
        rows = [[False for itr1 in xrange(9)] for itr2 in xrange(9)]
        cols = [[False for itr1 in xrange(9)] for itr2 in xrange(9)]
        grids = [[False for itr1 in xrange(9)] for itr2 in xrange(9)]
        for i in xrange(9):
            for j in xrange(9):
                if board[i][j] != '.':
                    idx = int(board[i][j]) - 1
                    rows[i][idx], cols[j][idx], grids[3*(i/3)+(j/3)][idx] = True, True, True
        return self.solveSudoku_rec(board, rows, cols, grids, 0)

    def solveSudoku_rec(self, board, rows, cols, grids, level):
        if level == 81:
            return True
        i, j = level / 9, level % 9
        if board[i][j] != '.':
            return self.solveSudoku_rec(board, rows, cols, grids, level+1)
        for k in xrange(1, 10):
            idx = k - 1
            if rows[i][idx] or cols[j][idx] or grids[3*(i/3)+(j/3)][idx]:
                continue
            rows[i][idx], cols[j][idx], grids[3*(i/3)+(j/3)][idx] = True, True, True
            succ = self.solveSudoku_rec(board, rows, cols, grids, level+1)
            if not succ:
                rows[i][idx], cols[j][idx], grids[3*(i/3)+(j/3)][idx] = False, False, False
            else:
                return succ
        return False
</pre>
