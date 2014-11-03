---
layout: post
title: LeetCode | Evaluate Reverse Polish Notation in Java
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
    1. 遇到数字压入栈中
    2. 遇到运算符，弹出栈中头两个元素进行相应运算
*/
public class Evaluate_Reverse_Polish_Notation{

    public int evalRPN(String[] tokens) {
        if(tokens == null || tokens.length == 0) return 0;
        Deque<Integer> deque = new ArrayDeque<Integer>();
        HashSet<String> ops = new HashSet<String>();
        Collections.addAll(ops, "+", "-", "*", "/");
        for(String str : tokens){
            if(!ops.contains(str)){
                deque.push(Integer.valueOf(str));
            }else{
                int op1 = deque.pop();
                int op2 = deque.pop();
                if(str.equals("+")) {
                    deque.push(op1+op2);
                }else if(str.equals("-")){
                    deque.push(op2 - op1);
                }else if(str.equals("*")){
                    deque.push(op1*op2);
                }else{
                    deque.push(op2 / op1);
                }
            }
        }
        return deque.pop();
    }
}
</pre>
