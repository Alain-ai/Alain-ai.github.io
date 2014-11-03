---
layout: post
title: LeetCode | Binary Tree Inorder Traversal in Python
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
    Given a binary tree, return the inorder traversal of its nodes\' values.

Algorithm:
    Morris traversal
'''


class Solution:
    # @param root, a tree node
    # @return a list of integers
    def inorderTraversal(self, root):
        res = []
        cur = root
        while cur:
            if not cur.left:
                res.append(cur.val)
                cur = cur.right
            else:
                tmp = cur.left
                while tmp.right and tmp.right != cur:
                    tmp = tmp.right
                if not tmp.right:
                    tmp.right = cur
                    cur = cur.left
                else:
                    tmp.right = None
                    res.append(cur.val)
                    cur = cur.right
        return res
</pre>
