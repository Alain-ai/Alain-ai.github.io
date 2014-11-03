---
layout: post
title: LeetCode | LRU Cache in Java
categories: LeetCode
tags: Java

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


<pre>
/*
    1. 继承LinkedHashMap，LinkedHashMap实现了按照访问顺序进行排列
*/
public class LRUCache extends java.util.LinkedHashMap<Integer, Integer> {

    private int capacity;
    private int count = 0;

    public LRUCache(int capacity) {
        super(10, 0.75f, true);
        this.capacity = capacity;
    }

    @Override
    public Integer get(Object key) {
        if(!super.containsKey(key)){
            return -1;
        }else{
            return super.get(key);
        }
    }

    public void set(Integer key, Integer value) {
        if(!super.containsKey(key)){
            if(count == capacity){
                --count;
                Integer keyDel = super.keySet().iterator().next();
                super.remove(keyDel);
            }
            super.put(key, value);
            ++count;
        }else{
            super.put(key, value);
        }
    }
}
</pre>
