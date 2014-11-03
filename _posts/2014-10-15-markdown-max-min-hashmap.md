---
layout: post
title: Max-Min HashMap
categories: algorithm
tags: Java

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

Let's implement a generic class MaxMinHashMap which extends from HashMap and additionally has getMinValue and getMaxValue method.

To accomplish this, we have to consider the following things:

1. What kind of type can be passed as key and value?
2. All values should be compared in order to get max and min.
3. How can we get max or min?

There are two ways to think about (3). One is to compute one of them by iterating over all values stored in the object; the other one is to maintain max and min at running time and change them if necessary.

Let's try to implement it in a simple way.

<pre>
public class MinMaxHashMap< K, V extends Comparable< V > > extends HashMap< K, V >{

    public V getMax(){
        Collection< V > vs = this.values();
        if (vs.size() == 0) {
            return null;
        }else {
            Iterator< V > itr = vs.iterator();
            V max = itr.next();
            while(itr.hasNext()){
                V next = itr.next();
                max = max.compareTo(next) > 0 ? max : next;
            }
            return max;
        }
    }

    public V getMin(){
        Collection< V > vs = this.values();
        if (vs.size() == 0) {
            return null;
        }else {
            Iterator< V > itr = vs.iterator();
            V min = itr.next();
            while(itr.hasNext()){
                V next = itr.next();
                min = min.compareTo(next) < 0 ? min : next;
            }
            return min;
        }
    }
}
</pre>


Note that

1. Values that might be passed in should implements Comparable interface and this is guaranteed by "V extends Comparable< V > ".
2. Values are stored in a collection and the only way to access is iterator.
