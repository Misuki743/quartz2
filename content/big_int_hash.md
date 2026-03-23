---
title: About bigint hash
---

Consider the following problem:

> Given an array $$A = [A_1, A_2, A_3, \ldots]$$ consist of $$N$$ integers ($$1 \leq A_i \leq 10^{2 \times 10^5}$$), process the following query $$Q$$ times ($$Q \leq 2 \times 10^5$$):
>
> - Given a tuple of integers $$(i, j, k)$$, check whether $$A_i + A_j = A_k$$.

Our goal is to handle each query in $$O(1)$$.

### Solution:

Let $$P$$ be a random prime in $$[2^{60}, 2^{61}]$$, to check whether $$A_i + A_j = A_k$$, we check $$A_i + A_j \equiv A_k \pmod P$$ instead, if we precompute $$A_i \pmod P$$ first, each query can be handled in $$O(1)$$.

### Probability analysis:

The above algorithm would fail only when $$A_i + A_j \neq A_k$$ but $$A_i + A_j \equiv A_k \pmod P \Leftrightarrow P \mid (A_k - (A_i + A_j)) = X$$.

Since there are about $$\frac{2^{60}}{\log(2^{60})}$$ primes in $$[2^{60}, 2^{61}]$$ by prime number theorem, and the maximum number of prime divisor in $$[2^{60}, 2^{61}]$$ $$X$$ can have is bounded by $$\log_{2^{60}}(X)$$, the probability that $$P \mid X$$ hold would be around $$\frac{\log(2^{60})\log_{2^{60}}(X)}{2^{60}} \approx 10^{-13}$$.

And since there are $$Q$$ queries, the probability that all of them are not failed is $$(1 - 10^{-13})^Q = \sum\limits_{i = 0}^Q \binom{Q}{i}(-10^{-13})^i \approx \binom{Q}{0} - \binom{Q}{1} \times 10^{-13} \approx 1 - 10^{-8}$$, so the fail probability is $$10^{-8}$$ per test case, which should be small enough.

### Side note

Sometime problem would ask for something like

- the number of distinct $$A_i + A_j$$ over all $$i < j$$
- use $\pmod P$ as hash function to build hash table over $$A$$

which made $$O(N^2)$$ comparison implicitly, and $$Q = N^2$$ should be used in such situation.

### A few relevent past problems

[ABC339F - Product Equality](https://atcoder.jp/contests/abc339/tasks/abc339_f)

[ARC216C - Count Power of 2](https://atcoder.jp/contests/arc216/tasks/arc216_c)

[The 3rd Universal Cup. Stage 7: Warsaw pF - Fibonacci Fusion](https://qoj.ac/contest/1774/problem/9225)
