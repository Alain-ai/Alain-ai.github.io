---
layout: post
title: LeetCode | Clone Graph in Python
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
    Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.

Algorithm:
    "cloneGraph_rec" get a node and return its cloned node and try to fill the cloned node's neighbors with other new cloned nodes
'''


class Solution:
    # @param node, a undirected graph node
    # @return a undirected graph node
    def cloneGraph(self, node):
        return self.cloneGraph_rec(node, {})

    def cloneGraph_rec(self, node, visited):
        if node in visited:
            return visited[node]
        node_new = UndirectedGraphNode(node.label)
        node_new.neighbors = []
        visited[node] = node_new
        for n in node.neighbors:
            n_new = self.cloneGraph_rec(n, visited)
            node_new.neighbors.append(n_new)
        return node_new
</pre>
