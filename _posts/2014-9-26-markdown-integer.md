---
layout: post
title: Java Source Code - Integer
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

In a previous blog, Integer's property of immutability has been discussed extensively. Basically, immutability is implemented by some declarations involving with private and final variable and even the way of just exposing a getting interface.

In this blog, we plan to discuss more.
First, let's focus on the amazing implementation of "toString" method. The source code is shown following:
<pre>
  public static String toString(int i) {  
    if (i == Integer.MIN_VALUE)  
      return "-2147483648";  
    int size = (i < 0) ? stringSize(-i) + 1 : stringSize(i);  
    char[] buf = new char[size];  
    getChars(i, size, buf);  
    return new String(buf, true);  
  }
</pre>

- The reason for dealing with the special case of Integer.MIN_VALUE is that it does not have the corresponding absolute value. Note that the range of Integer(int) is from $-2^{31}$ to $2^{31}-1$.

Then we go deeper insider to take a look at getChars method. It looks like as following:
<pre>
  static void getChars(int i, int index, char[] buf) {  
    int q, r;  
    int charPos = index;  
    char sign = 0;  
    // here is why Integer.MIN_VALUE lets getChars fail,  
    if (i < 0) {  
      sign = '-';  
      i = -i;  
    }  
    // Generate two digits per iteration  
    while (i >= 65536) {  
      q = i / 100;  
      r = i - ((q << 6) + (q << 5) + (q << 2));  
      i = q;  
      buf [--charPos] = DigitOnes[r];  
      buf [--charPos] = DigitTens[r];  
    }  
    // Fall thru to fast mode for smaller numbers  
    // assert(i <= 65536, i);  
    for (;;) {  
      q = (i * 52429) >>> (16+3);  
      r = i - ((q << 3) + (q << 1)); // r = i-(q*10) ...  
      buf [--charPos] = digits [r];  
      i = q;  
      if (i == 0) break;  
    }  
    if (sign != 0) {  
      buf [--charPos] = sign;  
    }  
  }
</pre>

- The first trick used here is at line 13. We show that $100=64+32+4=2^6+2^5+2^2$. Note that if you have to multiply a moderately large number many times, this trick is highly recommended to apply.
- After line 13, it is actually the last two digits of i. Then owing to two pre-defined tables, we are able to get the corresponding digit in constant time. The underlying idea is to cope with two digits at one time. For example, the last two digits are 27.  DigitOnes[27] returns 7 and DigitTens[r] returns 2.
<pre>
    final static char [] DigitTens = {  
        '0', '0', '0', '0', '0', '0', '0', '0', '0', '0',  
        '1', '1', '1', '1', '1', '1', '1', '1', '1', '1',  
        '2', '2', '2', '2', '2', '2', '2', '2', '2', '2',  
        '3', '3', '3', '3', '3', '3', '3', '3', '3', '3',  
        '4', '4', '4', '4', '4', '4', '4', '4', '4', '4',  
        '5', '5', '5', '5', '5', '5', '5', '5', '5', '5',  
        '6', '6', '6', '6', '6', '6', '6', '6', '6', '6',  
        '7', '7', '7', '7', '7', '7', '7', '7', '7', '7',  
        '8', '8', '8', '8', '8', '8', '8', '8', '8', '8',  
        '9', '9', '9', '9', '9', '9', '9', '9', '9', '9',  
        } ;  
    final static char [] DigitOnes = {  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
        '0', '1', '2', '3', '4', '5', '6', '7', '8', '9',  
    } ;
</pre>
- The number 52429 looks so wired here. In fact, it comes from $\lceil \frac{2^{16+3}}{10}\rceil$. What line 21 aims to do is $q = i * 0.1$.
- But as we can see, i is probably $65537$ and therefore $65537\*52429=3436039373$. Overflow! However, surprisingly, $$(65537\*52429)>>>19=6553.$$ Even overflow affects nothing. However again, if we set i as $80000$,  $$(80000*52429)>>>19 \ne 8000$$.
- I also try to do some potential improvements based on this code. I find we can continue to pull down the line before we stop the phase of deal with two digits at one time. I set is as 1024. Then the line 21 becomes
<pre>
  q = (i * 3355444) >>> (25);  
</pre>
- Some simple experiments have been performed and I find this modification indeed improves a little bit.
