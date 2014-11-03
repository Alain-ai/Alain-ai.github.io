---
layout: post
title: LeetCode | LRU Cache in Python
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
    Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set.

    get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
    set(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

Algorithm:
    doubly linkedlist + dict
    setting dummy head and tail makes operations easier
'''


class Entry:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

    def __repr__(self):
        return str(self.val)


class LRUCache:

    # @param capacity, an integer
    def __init__(self, capacity):
        self.capacity = capacity
        self.head = Entry(0, 0)
        self.tail = Entry(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head
        self.mapper = dict()
        self.count = 0

    # @return an integer
    def get(self, key):
        if key not in self.mapper:
            return -1
        else:
            self.move_to_head(self.mapper[key])
            return self.mapper[key].val

    # @param key, an integer
    # @param value, an integer
    # @return nothing
    def set(self, key, value):
        if key not in self.mapper:
            node = Entry(key, value)
            self.mapper[key] = node
            if self.count == self.capacity:
                self.mapper.pop(self.tail.prev.key, None)
                p = self.tail.prev
                node.next = p.next
                node.prev = p.prev
                p.prev.next = node
                self.tail.prev = node
            else:
                p = self.tail.prev
                p.next = node
                node.prev = p
                self.tail.prev = node
                node.next = self.tail
                self.count += 1
            self.move_to_head(self.tail.prev)
        else:
            node = self.mapper[key]
            node.val = value
            self.move_to_head(node)

    def move_to_head(self, node):
        if node.prev == self.head:
            return
        else:
            p, n = node.prev, node.next
            p.next = n
            n.prev = p
            hn = self.head.next
            self.head.next = node
            node.prev = self.head
            node.next = hn
            hn.prev = node
</pre>
