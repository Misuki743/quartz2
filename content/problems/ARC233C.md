# Equal Degree Deletion

**Problem.** A tree is good if we can delete all of its edges with the following operation:

- Choose a edge connect to two vertices with same degree and delete it.

Given a tree with $N$ vertices, count the number of good connected subgraph. ($N \le 3 \times 10^5$)

**Observation 1. (In a global view)**

To decide a good tree, we can keep deleting a perfect matching on the subgraph induced by set of vertices with maximum degree until all edges are deleted.

**Observation 2. (In a local view)**

Consider all edges incident to a vertex $v$, (\*) the set of degree of $v$ right before the deletion of these edges must be exactly $[\text{deg}(v)]$, if we label each edge with such value, then the tree is valid iff this labeling satisfy (\*) for all vertices. Also **Observation. 1.** imply each valid tree have unique edge labeling.

**What's the worst case?**

Then we can derive a DP method by maintain the mask of edge labels used in edges connect to children. But it seems slow if implemented directly.

Since for a valid tree to have edge label $h$, size of such tree must be at least $2^{h}$. Thus we may suspect that lot of computation is redundant?

If for a subtree with max label $h$, we only use $O(h\cdot 2^h)$ times to add this contribution to parent, the total complexity would be $O(\sum h(v) \cdot 2^{h(v)})$.

Consider maximize occurence of subtree with max label $h$, we can start from a such subtree, and reuse it everytime we generate a new subtree with label $h$, then we need to connect it with subtrees with label $\{1, 2, \ldots, (h - 1)\}$, thus connecting with $\Omega(2^h)$ vertices, so the total contribution for such subtree is $O(n\log n)$ and the total complexity is $O(n\log^2 n)$.
