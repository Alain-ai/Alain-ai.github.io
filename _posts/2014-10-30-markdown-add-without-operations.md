---
layout: post
title: Add Without Operations
categories: algorithm
tags: Other

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

Implement addition of two non-negative numbers without using "+", "-", "*" and "/".

Function "addOneAtI" adds one at the ith digit of binary number "a".

<pre>
public class AddWithoutOps {

    public int addWithoutOps(int a, int b){
        for (int i = 0; i < 31; ++i){
            if (((b >> i) & 1) == 1){
                a = addOneAtI(a, i);
            }
        }
        return a;
    }

    public int addOneAtI(int a, int i){
        if (i >= 31){
            return a;
        }
        if (((a >> i) & 1) == 0) {
            return a | (1 << i);
        }else {
            return addOneAtI((a ^ (1 << i)), i+1);
        }
    }
}
</pre>
