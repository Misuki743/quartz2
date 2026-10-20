**Problem.** Given a string $s$ consist of "ABCD", consider the following operation:

- choose a substring that is rotation of "ABCD", and rotate it arbitrarilly.

Find the number of possible string can be obtained by doing such operation any number of times.

**Full solution.**

First consider the transformation $s_i = (s_i - A) \pmod{4}$, and consider algorithm $\mathcal{A}$ similar to decide whether a bracket sequence is RBS, then a string can be decompose into some single element block and block with $4$ equal elements, and they forms a bracket sequence-like structure.

***How does the set of reachable strings looks like?***

Let $k$ be the number of non-singular block $s$ have, then one can notice that the set of reachable strings are exactly those obtained by inserting $k$ blocks of $4$ equal elements into the string consist of all singular blocks of $s$, preserving this order.

Then the problem can be rephrased as follows:

- Given a string consist of "0123", consider insert $k$ length $4$ string of equal numbers, find the number of possible result strings.

Consider the case where the given string is empty. A string may be obtained by multiple ways of insertion and numbers are matched differently.

***Build bijection between strings and its block decomposition***

Though there may exist multiple ways to decompose a string into blocks, we can distinguish each string by its decomposition obtained by the algorithm $\mathcal{A}$, then we've build a bijection between such decomposition and strings.

***Counting***

For each string $s$, consider the block $(i_1 = 1, i_2, i_3, i_4)$, and decompose the strings into smaller pieces.

Without loss of generality, assume $s_1 = 0$, then structure of $s$ would looks like $0 + SEQ(\mathcal{F'}) + 0 + SEQ(\mathcal{F'}) + 0 + SEQ(\mathcal{F'}) + 0 + \mathcal{F}$. Where $\mathcal{F}$ denote the set of blocks where the first and last element belongs to the outtermost block. (Kind of like bracket sequences where the first element match to the last element)

And $\mathcal{F'}$ is those blocks with first element not equal to $0$. Such constraint is imposed by the assumption that the block decomposition is a greedy decomposition obtained by $\mathcal{A}$.

Then we can derive recursion relation between $\mathcal{F}, \mathcal{F'}, SEQ(\mathcal{F'})$ and everything can be calculated by DP in $O(|s|^3)$ and the case where some single element block exist is trivial and left as an exercise.
