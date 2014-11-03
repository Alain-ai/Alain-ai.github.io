---
layout: post
title: Singleton
categories: Design_Pattern
tags: Java

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

Singleton Pattern requires there is only one instance of a class allowed. There exist three obvious features in a singleton class.

1. private construtor
2. private static reference
3. public static "getInstance" method

Here is a basic example that works in regular environment.

## Example 1
<pre>
public class A {

    private static A a;

    private A() {}

    public static A getInstance() {
        if (a == null) {
            a = new A();
        }
        return a;
    }
}
</pre>


Note that example 1 only works at the single thread setting. When it comes to the multi-thread environment, more than one instance still can be created. Thus we try to improve example 1 to fit the multi-thread situation.

## Example 2
<pre>
public class A {

    private static A a;

    private A() {}

    private static final Object obj = new Object();

    public static A getInstance() {
        synchronized (obj) {
            if (a == null) {
                a = new A();
            }
        }
        return a;
    }
}
</pre>


In example 2, every execution of "getInstance" will add a locker on "obj", which could be inefficient. Can we do better? We need a mechanism to let a statement or a block of statements run only once. Java really provides us something like this. It's "static block". The following example shows how it looks like.


## Exmaple 3
<pre>
public class A {

    static{
        a = new A();
    }

    private static A a;

    private A() {}

    public static A getInstance() {
        return a;
    }
}
</pre>
