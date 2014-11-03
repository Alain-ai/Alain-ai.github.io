---
layout: post
title: LeetCode | Valid Sudoku in Python
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
    Determine if a Sudoku is valid, according to Sudoku Puzzles - The Rules. The Sudoku board could be partially filled, where empty cells are filled with the character ".".

Algorithm:
    DFS
    in "grids", we just use the ith row to flag the ith 3*3 grid
'''


class Solution:
    # @param board, a 9x9 2D array
    # @return a boolean
    def isValidSudoku(self, board):
        rows = [[False for itr1 in xrange(9)] for itr2 in xrange(9)]
        cols = [[False for itr1 in xrange(9)] for itr2 in xrange(9)]
        grids = [[False for itr1 in xrange(9)] for itr2 in xrange(9)]
        for i in xrange(9):
            for j in xrange(9):
                if board[i][j] == '.':
                    continue
                num = int(board[i][j]) - 1
                if rows[i][num] or cols[j][num] or grids[(i/3)*3+(j/3)][num]:
                    return False
                else:
                    rows[i][num], cols[j][num], grids[(i/3)*3+(j/3)][num] = True, True, True
        return True
</pre>
