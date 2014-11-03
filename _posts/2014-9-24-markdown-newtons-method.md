---
layout: post
title: Newton's Method
categories: Machine_Learning
tags: Machine_Learning

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
jax: ["input/TeX","output/HTML-CSS"],
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]},
extensions: ["tex2jax.js","MathMenu.js","MathZoom.js"],
TeX: { equationNumbers: { autoNumber: "AMS" }, extensions: ["AMSmath.js", "AMSsymbols.js","noErrors.js","noUndefined.js"]}
});
</script>

<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
</script>


First note that we have Newton's Method in calculus and in optimization. Generally, Newton's Method is the one in calculus, which aims to find $x^\*$ such that $f(x^\*)=0$.

Suppose we are now at $x = x^\* + h$ and expanding $f(x)$ at point $x^\*$. We will get
\begin{equation}
f(x) = f(x^\*+h) = f(x^\*) + f'(x^\*)h
\end{equation}


Since $f(x^\*)=0$, (1) becomes $f(x) = f'(x^\*)h$. Then $h = \frac{f(x)}{f'(x^\*)}$. To update, we set the new $x'$ as $x-h=x- \frac{f(x)}{f'(x^*)}$.

Because we have to get $f'(x^*)$, which is basically impossible to do, this method doesn't work.

Then we alter to expand $f(x^\*)$ at point $x$, that is

\begin{align}
f(x^*) = f(x-h) & = f(x) + f'(x)(-h) \\ \newline
&= f(x) + f'(x)(-h) + \frac{1}{2}f''(x)h^{2}
\end{align}
for first moment and second moment expansion.



In terms of (2), we have
$$
f(x^{\*}) = 0 = f(x) + f'(x)(-h) \implies h = \frac{f(x)}{f'(x)}.
$$
So, the new $x'$ will be updated as $x-h = x - \frac{f(x)}{f'(x)}.$

If we consider (3), we will get

\begin{align\*}
f(x^{\*}) = 0  & = f(x) + f'(x)(-h) + \frac{1}{2}f''(x)h^{2} \\ \newline
& \implies h = \frac{f'(x) \pm \sqrt{(f'(x))^{2} - 2f''(x)f(x)}}{f''(x)}
\end{align\*}

Since we have multiple choices to update $x$, this method actually won't work.

The convergence of Newton's Method. As before, we also expand $f(x^{\*})$ at the current $x$. We get
\begin{align}
f(x^{\*}) = 0 = f(x) + f'(x)(x^{\*}-x) + \frac{1}{2}f''(x)(x^{\*}-x)^{2}
\end{align}
Suppose this second-order approximation is good enough, which requires $x$ is not too far away from $x^{\*}$ originally.
Then we divide (4) by $f'(x)$(assume that $f'(x) \ne 0$), we will have
\begin{align}
\frac{f(x)}{f'(x)} + x^{\*} - x = -\frac{f''(x)}{2f'(x)}(x^{\*} - x)^{2}
\end{align}
Note that the new $x'$ is going to be updated as $x - \frac{f(x)}{f'(x)}$. (5) therefore becomes
\begin{align\*}
x^{\*} - x'  & = -\frac{f''(x)}{2f'(x)}(x^{\*} - x)^{2} \\ \newline
& \implies |x^{\*} - x'| = |\frac{f''(x)}{2f'(x)}| \* |x^{\*} - x|^{2}
\end{align\*}
Denote $|x^{\*} - x'|$ as $\Delta'$ and $|x^{\*} - x|$ as $\Delta$. We get
\begin{align}
\Delta' = |\frac{f''(x)}{2f'(x)}|\Delta ^{2}
\end{align}
(6) shows the rate of convergence is quadratic if

1. $f'(x) \ne 0$
2. $f''(x)$ is finite
3. $x^{(0)}$(the initial guess) should be sufficiently close to $x^{\*}$.

Note that there exists disparity of Newton's Method in between calculus and optimization.
Newton's Method in calculus aims to find $x^{\*}$ such that $f(x^{\*}) = 0$.
While in terms of optimization field, we actually would like to maximize(or minimize) $f(x)$. The problem ends up finding $x^{\*}$ such that $f'(x^{\*}) = 0$.

The following is an easy way to conceptually understand Newton's Method in optimization.
If we denote $f'(x)$ as $g(x)$ and then use Newton's Method to solve $x^{\*}$ such that $g(x^{\*}) = 0$.
Thus we will have the following update rule:
$$
x^{(n+1)} = x^{(n)} - \frac{g(x^{(n)}}{g'(x^{(n)})}
$$
Put $f'(x)$ back, we get
$$
x^{(n+1)} = x^{(n)} - \frac{f'(x^{(n)}}{''(x^{(n)})}
$$

Note that Quasi-Newton Method is another way to optimize, which won't explicitly compute the second-order derivative.
