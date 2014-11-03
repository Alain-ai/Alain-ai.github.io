---
layout: post
title: Hash Function
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


## Many
Hash function for String and other classes that have multiple variables such as List is defined recursively. However, they are not completely the same.

## String hash
The code for String's hash function is shown as following:
<pre>
  public int hashCode() {
    int h = hash;
    if (h == 0 && value.length > 0) {
      char val[] = value;
      for (int i = 0; i < value.length; i++) {
        h = 31 * h + val[i];
      }
      hash = h;
    }
     return h;
  }
</pre>

The computational strategy is
$$s[0]\*31^{(n-1)} + s[1]\*31^{(n-2)} + ... + s[n-1],$$ where $s$ is the underlying char array of the String object. $s[i]$ is the corresponding char value.
We are also able to find out that the hash value for a String object is going to be calculated and **stored only once**.

## List hash
Then the code for List's hash function is followed as:
<pre>
  public int hashCode() {
    int hashCode = 1;
    for (E e : this)
      hashCode = 31\*hashCode + (e==null ? 0 : e.hashCode());
  return hashCode;
  }

</pre>
It is defined recursively as
$$31^{n} + v_0\*31^{(n-1)} + v_1*31^{(n-2)} + ... + v\_{n-1},$$
 where $v_0, v_1, ..v\_{n-1}$ are the variables. Without having the property of immutability of String, $v_1, v_2, ...v_{n-1}$ might change during running time. Thus at each time when hash function is called, the hash value will be **recalculated** as above.

## Array hash
How about Array?
Let's boil down some essence from the following code.
<pre>
    Integer [] is1 = new Integer[]{1};
    Integer [] is2 = new Integer[]{1};
    ArrayList<Integer> ls1 = new ArrayList<Integer>(Arrays.asList(is1));
    ArrayList<Integer> ls2 = new ArrayList<Integer>();
    ls2.add(1);
    System.out.println(is1.hashCode());
    System.out.println(is2.hashCode());
    System.out.println(Arrays.hashCode(is1));
    System.out.println(ls1.hashCode());
    System.out.println(ls2.hashCode());
</pre>
The result is as

+ 481088980
+ 386555905
+ 32
+ 32
+ 32

The reason why two random number "481088980" and "386555905" show up is that actually the native Object's hash function has been called. "Native" represents the implementation involves with the platform. A standard way to obtain the hash value of a array is Arrays.hashCode(), which looks like
<pre>
public static int hashCode(Object a[]) {
  if (a == null)
    return 0;
  int result = 1;
  for (Object element : a)
    result = 31 * result + (element == null ? 0 : element.hashCode());
  return result;
}
</pre>

It's easy to know hash functions for List and Array actually encodes the same idea to compute hash value.
32 follows from $31^1 + 1 * 31^0 = 32$ for "is1", "ls1" and "ls2".
