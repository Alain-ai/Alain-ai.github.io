---
layout: post
title: LeetCode | Valid Palindrome in Python
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
    Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases. For example,
    1. "A man, a plan, a canal: Panama" is a palindrome.
    2. "race a car" is not a palindrome.

Algorithm:
    squeeze to the middle from two ends and ignore all alphanumeric characters
'''


class Solution:
    # @param s, a string
    # @return a boolean
    def isPalindrome(self, s):
        i, j = 0, len(s) - 1
        while i < j:
            if ord('a') <= ord(s[i].lower()) <= ord('z') or ord('0') <= ord(s[i]) <= ord('9'):
                if ord('a') <= ord(s[j].lower()) <= ord('z') or ord('0') <= ord(s[j]) <= ord('9'):
                    if s[i].lower() == s[j].lower():
                        i, j = i + 1, j - 1
                    else:
                        return False
                else:
                    j -= 1
            else:
                i += 1
        return True
</pre>
