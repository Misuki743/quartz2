**Problem.** Construct a way to fill $1 \times 2$ dominoes into a $n \times n$ grid such that no pair of dominoes share a side or corner.

**Key Observation.**

The number of dominoes can be placed is at most $\lfloor\frac{(n+1)^2}{6}\rfloor$.

> [!proof]- proof
> 
> A domino would cover two full cells, six half cells and four corner of cells, so it cover $6$ full cells in total. And there are $n^2$ full cells, $4n$ half cells and $4$ cells with only corner, so there are $n^2 + 2n + 1 = (n + 1)^2$ full cells. So we can place at most $\lfloor\frac{(n+1)^2}{6}\rfloor$ dominos.

Then one can manually construct $n \le 6$ and for $n > 6$, try to fill the $n \times n$ grid without top-left $(n - 6) \times (n - 6)$ with $\frac{(n + 7)^2 - (n+1)^2}{6} = 2n + 8$ dominoes. Then we have finish all construction by induction.
