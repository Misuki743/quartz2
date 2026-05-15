---
title: About bigint hash
---

Consider the following problem:

> Given an array $$A = [A_1, A_2, \ldots]$$ consist of $$N$$ integers ($$1 \leq A_i \leq 10^{2 \times 10^5}$$), process the following query $$Q$$ times ($$Q \leq 2 \times 10^5$$)
>
> - Given a tuple of integers $$(i, j, k)$$, check whether $$A_i + A_j = A_k$$ hold.

Our goal is to handle each query in $$O(1)$$.

### solution

Let $$P$$ be a random prime in $$[2^{60}, 2^{61}]$$, to check whether $$A_i + A_j = A_k$$ hold, we check $$A_i + A_j \equiv A_k \pmod P$$ instead. If we precompute $$A_i \pmod P$$ first, each query can be handled in $$O(1)$$.

### probability analysis

The above algorithm would fail only when $$A_i + A_j \neq A_k$$ and $$A_i + A_j \equiv A_k \pmod P \Leftrightarrow P \mid (A_k - (A_i + A_j)) = X$$ hold.

Since there are about $$\frac{2^{60}}{\log(2^{60})}$$ primes in $$[2^{60}, 2^{61}]$$ by prime number theorem, and the number of prime divisor in $$[2^{60}, 2^{61}]$$ $$X$$ can have is bounded by $$\log_{2^{60}}(X)$$, the probability that $$P \mid X$$ holds would be around $$\frac{\log(2^{60})\log_{2^{60}}(X)}{2^{60}} \approx 10^{-13}$$.

And thus the probability that all of the queries does not fail is $$(1 - 10^{-13})^Q = \sum\limits_{i = 0}^Q \binom{Q}{i}(-10^{-13})^i \approx \binom{Q}{0} - \binom{Q}{1} \times 10^{-13} \approx 1 - 10^{-8}$$, so the fail probability is $$10^{-8}$$ per test case, which should be small enough.

In general, the fail probability is $$\frac{\log(U-D)\log_D(X)}{U-D} \times Q$$ (assume $$\frac{\log(U-D)\log_D(X)}{U-D} \ll Q$$), where $$P$$ is a prime randomly pick from $$[D, U]$$ and $$Q$$ is the total comparison made.

### side note

Some problem would ask for something like

- the number of distinct $$A_i + A_j$$ over all $$(i, j)$$
- use $\pmod P$ as hash function to build hash table over $$A$$

which made $$O(N^2)$$ comparison implicitly, and $$Q = N^2$$ should be used in such situation.

### relevant past problems

[ABC339F - Product Equality](https://atcoder.jp/contests/abc339/tasks/abc339_f)

[ARC216C - Count Power of 2](https://atcoder.jp/contests/arc216/tasks/arc216_c)

[The 2nd Universal Cup. Stage 20: Ōokayama pM - Sum is Integer](https://qoj.ac/contest/1499/problem/8177)

[The 3rd Universal Cup. Stage 7: Warsaw pF - Fibonacci Fusion](https://qoj.ac/contest/1774/problem/9225)

