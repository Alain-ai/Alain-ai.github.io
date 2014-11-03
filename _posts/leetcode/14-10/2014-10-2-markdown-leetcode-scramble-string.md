---
layout: post
title: LeetCode | Scramble String in Python
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
    Given a string s1, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively. Below is one possible representation of s1 = "great":

    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t
    To scramble the string, we may choose any non-leaf node and swap its two children. For example, if we choose the node "gr" and swap its two children, it produces a scrambled string "rgeat".

    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t
    We say that "rgeat" is a scrambled string of "great". Similarly, if we continue to swap the children of nodes "eat" and "at", it produces a scrambled string "rgtae".

    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a
    We say that "rgtae" is a scrambled string of "great". Given two strings s1 and s2 of the same length, determine if s2 is a scrambled string of s1.

Algorithm:
    to determine if s2 is a scrambled string of s1, we have to check split s1 into two parts at every possible position and do the same thing with s2 from two sides. And if there exists one splitting position to let the two parts of s1 and s2 match, we will get the result.
'''


class Solution:
    # @return a boolean
    def isScramble(self, s1, s2):
        return self.is_scramble_rec(s1, s2, 0, len(s1)-1, 0, len(s2)-1)

    def is_scramble_rec(self, s1, s2, stt1, end1, stt2, end2):
        if end1 - stt1 != end2 - stt2:
            return False
        if s1[stt1:end1+1] == s2[stt2:end2+1]:
            return True
        cnt = [0 for i in xrange(26)]
        for i in xrange(stt1, end1+1):
            cnt[ord(s1[i]) - ord('a')] += 1
        for i in xrange(stt2, end2+1):
            cnt[ord(s2[i]) - ord('a')] -= 1
        if any(cnt):
            return False
        for i in xrange(0, end1-stt1):
            return (self.is_scramble_rec(s1, s2, stt1, stt1+i, stt2, stt2+i) and self.is_scramble_rec(s1, s2, stt1+i+1, end1, stt2+i+1, end2)) or (self.is_scramble_rec(s1, s2, stt1, stt1+i, end2-i, end2) and self.is_scramble_rec(s1, s2, stt1+i+1, end1, stt2, end1-(stt1+i+1)+stt2))
        return False
</pre>
