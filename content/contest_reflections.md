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

Claim: If there exist non-adjacent pair touch each other, then there exist some bad element caused by only adjacent pairs.

Proof: Consider induction on length of array.

Assume $i$-th element and $j$-th element touch each other ($i < j, j - i > 1$), that is, $A_i + B_i > A_j - B_j$ holds.

1. If $j - i = 2$, $(i + 1)$-th element is bad and can be found by the relation between $(i, i + 1)$ and $(i + 1, j)$.
2. If $j - i > 2$, consider $(i + 1)$-th element. If $(i + 1)$-th element and $j$-th element doesn't touch each other, it would be completely covered by $i$-th element so checking relation between $(i, i + 1)$ is enough. Otherwise $(i + 1)$-th element and $j$-th element touch each other and thus the claim hold by the induction hypothesis.
