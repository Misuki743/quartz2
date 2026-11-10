**Problem.** There is a rooted tree, initially with one node. Consider repeat the following random process $K$ times:

- choose a leaf $l$ uniformly random, add $M$ nodes as its children.

Find the expected sum of depth of all nodes after the whole process. ($K \le 10^7$)

**Solution 1. (conditional expectation)**

Consider finding expected depth of nodes ($\mathbb{E}[D_i]$) added at $i$-th step.

By fixing a tree $T_{i-1}$, we have

$$\mathbb{E}[D_i \mid T_{i-1}] = \frac{\sum_{v \in L(T_{i - 1})} d(v)}{|L(T_{i-1})|} + 1 = \frac{\sum_{v \in L(T_{i - 1})} d(v)}{1 + (i - 1)(M - 1)} + 1$$

where $L(T)$ denote the set of leaves of tree $T$. Then by the property of conditional expectation, we have

$$\mathbb{E}[D_i] = \mathbb{E}[\mathbb{E}[D_i \mid T_{i - 1}]] = \frac{\mathbb{E}[\sum_{v \in L(T_{i - 1})} d(v)]}{1 + (i - 1)(M - 1)} + 1$$

So the problem reduced to finding expected sum of depth of leaves at $i$-th step.
For convenient, let $\mathbb{E}[LD_i]$ denote $\mathbb{E}[\sum_{v \in L(T_i)} d(v)]$.

Again, fix a tree $T_{i-1}$, we have

$$\mathbb{E}[LD_i | T_{i - 1}] = \sum_{v \in L(T_{i - 1})}d(v) + \frac{\sum_{v \in L(T_{i - 1})} (M - 1)d(v)}{1 + (i - 1)(M - 1)} + M = \frac{1 + i(M - 1)}{1 + (i - 1)(M - 1)}\mathbb{E}[LD_{i - 1} | T_{i - 1}] + M$$

$$\mathbb{E}[LD_i] = \mathbb{E}[\mathbb{E}[LD_i | T_{i - 1}]] = \frac{1 + i(M - 1)}{1 + (i - 1)(M - 1)}\mathbb{E}[LD_{i - 1}] + M$$

Then $$\mathbb{E}[LD_i]$$ is a linear recurrence and can be calculated directly, so $$\mathbb{E}[D_i]$$ can also be calculated directly and the problem is solved.

**Solution 2. (Polya's urn)**

Consider rephrase depth of a node as the number of edges from root to it, then sum of depth can be repharse as sum of subtree size over non-root nodes.

Assume we have $X$ trees with one node. When picking a node at $i$-th step and add $M$ child to it, the expected subtree size of newly added node after all $K$ operations are done is $1 + \frac{M (K - i)}{X + M - 1}$, by Polya's urn. Thus this step contribute $M + \frac{M^2 (K - i)}{X + M - 1}$ to the answer.

> [!Polya's urn]- Polya's urn
>
> Given a bag consist of $a$ red balls and $b$ blue balls initially, consider repeating the following process:
>
> - pick a ball from the bag uniformly random, put $M$ balls with same color back.
>
> **claim.** The probability that we pick a red ball at $i$-th step is $\frac{a}{a + b}$.
>
> > [!proof]- proof
> >
> > beyond separate balls by colors, consider also label them with distinct integers $\{1, 2, \ldots, a + b\}$. And when picking a ball from bag, we put $M$ balls with exact same color and label back.
> > Then different balls have exact same role and thus have same probability to be draw at any step.

Then in the next step, we reduce the problem into the case $X' = X + (M - 1)$. So the answer is $MK + \sum\limits_{i = 1}^K \frac{M^2(K - i)}{1 + i(M - 1)}$.
