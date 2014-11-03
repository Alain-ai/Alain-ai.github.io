---
layout: post
title: LeetCode | Binary Tree Preorder Traversal in Python
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
    Given a binary tree, return the preorder traversal of its nodes\' values.

Algorithm:
    Morris traversal
'''


class Solution:
    # @param root, a tree node
    # @return a list of integers
    def preorderTraversal(self, root):
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
                    res.append(cur.val)
                    tmp.right = cur
                    cur = cur.left
                else:
                    tmp.right = None
                    cur = cur.right
        return res
</pre>
