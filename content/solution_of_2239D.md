---
title: Solution documentation of CF2239D
---

[problem link](https://codeforces.com/contest/2239/problem/D)

Though the problem can be solved only by experience, I found myself getting stuck at multiple steps which should be standard, so I decide to write a documentation : )

### Solution

Since each vertex are symmetric, we can W.L.O.G. assume the the starting set is $\{1, \ldots, m\}$ and multiply final answer with $\binom{n}{m}$ at the end.

So problem can be described as follows:

> Given $N, M$, find the number of functional graph such that the following things are forbidden
> 1. self-loop
> 2. vertex $v > m$ being a leaf $\Leftrightarrow$ vertex $v > m$ have indegree $= 0$
> 3. "pure" cycle consist of only vertices $> m$

consider applying PIE on $2, 3$. (Actually I also included $1$ as condition of PIE but it become very terse and is not necessary because functional graph without self-loop also have a simple formula)

Assume we have $x$ leaves and $y$ vertices belongs to "pure" cycle. Then the answer is

$$\sum\limits_{x, y}\binom{n - m}{x, y, n - m - x - y} f(y) (n - x - y - 1)^{n - x - y}(n - x - y)^x(-1)^x$$

where $f(y)$ denote the total contribution over all possible ways to decompose set of $y$ vertices into "pure" cycles. Which is

$$\sum\limits_{c}\sum\limits_{k}\binom{y}{y - k}\genfrac{\lbrack}{\rbrack}{0pt}{}{y-k}{c}(-1)^c$$

Which turns out to be $1 - y$ by bruteforce.

So the above formula become

$$\sum\limits_{x, y}\binom{n - m}{x, y, n - m - x - y} (1-y) (n - x - y - 1)^{n - x - y}(n - x - y)^x(-1)^x$$

And let $s := x + y$, we have 

$$\sum\limits_s \binom{n - m}{s}(n-1-s)^{n-s}\sum\limits_x\binom{s}{x}(x-s+1)(s-n)^x$$

The formula inside $x$ looks like binomial theorem, let's decompose it further.

$$\sum\limits_x\binom{s}{x}(x-s+1)(s-n)^x = (1-s)\sum\limits_x\binom{s}{x}(s-n)^x + \sum\limits_x\binom{s}{x}x(s-n)^x$$

The first one is obviously $(1-s)(s - n + 1)^s$, and the problem is the second one (which made me stuck for a while)

But since $s$ is constant here, we can just absorb the variable $x$ into $\binom{s}{x}$ to make it like binomial theorem.

> Absorption Identity:
> $$\frac{n + 1}{m + 1}\binom{n}{m} = \binom{n + 1}{m + 1}$$

Which gives

$$\sum\limits_x \binom{s - 1}{x - 1}s(s - n)^x = s(s-n)\sum\limits_x \binom{s-1}{x-1}(s-n)^{x-1} = s(s-n)(s-n+1)^{s-1}$$

And the problem has been solved in $O(n\log n)$.
