---
title: Contest reflections
---

Just some reflection on problems

### ARC231C

**Problem.** Given $\{(A_i, B_i)\}_{i = 1}^{i = N}$, decide whether exist integer set $S$ s.t.

1. $A_i - B_i \in S$ or $A_i + B_i \in S$ holds for all $i$.
2. $x \notin S$ for all $i$ and $A_i - B_i < x < A_i + B_i$.

decide the answer after each point update on $B$.

**Key Step.**

The constraint feels very "local", is it sufficient to only check relation between adjacent terms?

**Claim.** It is sufficient to consider adjacent constraints to decide the **Problem**.

proof.

For convenience, Let $l_i$ denote $A_i - B_i$, $r_i$ denote $A_i + B_i$.

If one of the element strictly cover a adjacent element, we are done.

Otherwise both $\{l_i\}_{i = 1}^N$ and $\{r_i\}_{i = 1}^N$ would be non-decreasing.

Then if there exist $r_i > l_j, i < (j - 1)$, i.e. left end of $j$-th element is covered by $i$-th element. Consider the smallest $k \le j$ s.t. $l_k = l_j$, then we have

1. $r_k \ge r_i > l_j = l_{k + 1}$, so its right end is covered by $(k + 1)$-th element.
2. $l_k > l_{k - 1}$, so its left end is covered by $(k - 1)$-th element.
