---
layout: post
title: LeetCode | Binary Tree Postorder Traversal in Python
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
    def postorderTraversal(self, root):
        dummy = TreeNode(0)
        dummy.left = root
        cur = dummy
        res = []
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
                    res += self.trace_back(cur.left, tmp)
                    cur = cur.right
        return res

    def trace_back(self, frm, to):
        res = []
        cur = frm
        while cur is not to:
            res.append(cur.val)
            cur = cur.right
        res.append(to.val)
        res.reverse()
        return res
</pre>
