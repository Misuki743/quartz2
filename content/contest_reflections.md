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

If one of the element strictly cover a adjacent element, we are done.

Otherwise both $\{A_i - B_i\}_{i = 1}^N$ and $\{A_i + B_i\}_{i = 1}^N$ would be non-decreasing. So $i$-th element cover left end of $j$-th element imply $(j - 1)$-th element also cover left end of $j$-th element.
