**Problem.** Given a non-negative integer sequence $a_n$, find $\max\limits_{l \le r}(|\text{Unique}(a[l, r])| - \text{MEX}(a[l, r]))$. ($n \le 5 \times 10^5$)

**Key step.**

It is hard to evaluate MEX but easier to decide whehter MEX is no more than a certain value, and since we only want the maximum profit, underestimate won't cause any trouble.

Then we can enumerate such value $x$ and evaluate ($|\text{Unique}(a[l, r])| - x$) over all maximal subarrays not contain $x$.
