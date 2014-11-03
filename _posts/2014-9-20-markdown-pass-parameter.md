---
layout: post
title: Pass Parameters to A Function
categories: Language
tags: Java

---

<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

As we know, in java, a primitive-type variable is passed to a function by value while a Object-type variable is passed by its reference(i.e, the address to the memory where the real variable is stored).

But it should be kept in mind that the reference will never be passed back to the caller. We can just think this as a copy of reference is passed to the called method.

If the parameter alters to refer to other object in the called method, the corresponding variable(the block of memory) in the caller won't be affected. However, the memory which the parameter is pointing to gets changed in the called method, it will affect the world outside.

Here is an example to illustrate this.
<pre>
    class TryReferncenPassBack{  // some code we are not caring about this moment  
        int i;
    }

    class Test{

        public static void main(String [] args){
            TryReferncenPassBack t = new TryReferncenPassBack();
            t.i = 1;
            System.out.println(t.toString());
            System.out.println(t.i);
            method1(t);
            System.out.println(t.toString());
            System.out.println(t.i);
        }

        public static void method1(TryReferncenPassBack t){
            t.i = 2;
            t = new TryReferncenPassBack();
            System.out.println(t.toString());
            t.i = 3;
        }
    }
</pre>

Result:
<pre>
    TryReferncenPassBack@510bfe2c
    1
    TryReferncenPassBack@6a5c2445 // point to the new object
    TryReferncenPassBack@510bfe2c // after getting back, the reference still remains
    2 // the original memory gets changed at line 16 instead of line 19
</pre>
