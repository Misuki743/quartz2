**Problem.** Given $n\times n$ matrix $a$ with non-negative integers, except $a_{i, i} = a_{1, j} = a_{i, 1} = -1$, construct a $n$-vertex graph $G$ such that $a_{i, j} \neq -1 \Rightarrow |E(G[V - \{i, j\}])| = a_{i, j}$, the solution is guranteed to exist.

**Solution.**

For convenience, let $E$ denote size of edge set of $G$, $r_i(i > 1)$ denote $\sum\limits_{j > 1, j \neq i} a_{i, j}$, $d(i)$ denote degree of vertex $i$, $(i, j)$ denote $1$ if $G$ have $(i, j)$ as edge or $0$ otherwise.

Obviously $a_{i, j} = E - d_i - d_j + (i, j)$ hold.

***Key idea.***

Consider sum over a row, then we have

$$a_{i, 1} + r_i = (n - 1)E - (n - 1)d_i - \sum_{j \neq i}d_j + \sum_{j \neq i} (i, j)$$

which can be simplify by handshaking lemma, result in

$$(E - d_i - d_1 + (1, i)) + r_i = (n - 1)E - (n - 1)d_i - (2E - d_i) + d_i$$

$$d_i = E + \frac{r_i - d_1 + (1, i)}{n - 4}$$

***Further cleanup.***

Then for $n \ge 6$, after decide $d_1$, existence of all edges adjacent to $1$ is uniquely fixed $\Rightarrow d_1$ is fixed, and each $d_i$ has the form of $E + c_i$ for some constant $c_i$.

Sum over $d_i$ again gives us $E$ by handshaking lemma and then all $d_i$ are fixed, finally by the relation $a_{i, j} = E - d_i - d_j + (i, j)$, all edges are fixed.

So we can guess a $d_1$ and verify for the respective $G$, since there is only $O(1)$ possible $d_1$ to make all $d_i$ integer, the total time complexity is $O(n^2)$.

Note. The only hard idea here is to consider summing $a$ in a row, which reduce some information but also gives a clearer image on the problem model. (which feels like taking quotient of a group in abstract algebra?)
