---
layout: post
title: Bloom Filter
categories: Algorithm
tags: Other
---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


## Limitation
Bloom Filter does not support deletion operation
deletion operation might affect other objects

## False Positive
Bloom Filter might have false positive
all slots that the new object is going to set have been already 1
thus, Bloom Filter will think this new object has already been seen

## Parameters
We have several parameters for this algorithm

+ n: number of bits available
+ S: number of objects to be stored
+ k: number of hash function to be used
+ c: number of bits for per object
+ where n = S \* c


## Why it works
Consider the totally random situation, the probability of some slot to be 1 after S objects have been inserted into

- for one object and one hash function, the probability to be 0 is $(1-\frac{1}{n})$
- after S objects have been inserted and each of which uses k hash functions, the probability to be 0 is
$(1-\frac{1}{n})^{k\*S}$
- thus the probability to be 1 is
$1 - (1-\frac{1}{n})^{k\*S}$

Because
$\lim\limits_{n \rightarrow \infty}(1+\frac{1}{n})^{n} = e,$ then we will have
$$ 1 - (1-\frac{1}{n})^{k\*S} = 1-(1-\frac{1}{n})^{\frac{k\*n}{c}}<1-e^{\frac{-k}{c}},$$

which means the probability to be
$1 < 1 - e^{\frac{\-k}{c}}.$ For a new object, the probability of all bits having been set as
$ 1 < (1 - e^{\frac{-k}{c}})^{k}.$

To minimize $ (1 - e^{\frac{-k}{c}})^{k},$
enlarge c as much as possible
when $k = \ln(2) \* c,$ it will be minimized.

## Implementation
A good implementation can be found at [here](https://github.com/MagnusS/Java-BloomFilter/blob/master/src/com/skjegstad/utils/BloomFilter.java).
