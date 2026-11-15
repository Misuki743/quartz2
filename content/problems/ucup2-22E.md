**Problem.** Given strings $s_1, s_2, \ldots, s_n$, consist of lowercase alphabet, construct a way to shuffle characters in each string such that $s_i$ is period of $s_{i + 1}$ for all $i$. ($\sum|s_i| \leq 5 \times 10^6, n \leq 10^5$)

**Observation 1.** once $s_1$ is decided, all strings are decided.

**Observation 2.** $s_i$ can be a period of $s_{i+1}$ by shuffling iff

1. $f(s_{i + 1}, c) \ge f(s_i, c) * \lfloor\frac{|s_{i+1}|}{|s_i|}\rfloor$ for all $c \in \sum$
2. multiset of last $(|s_{i + 1}| \bmod |s_i|)$ characters of $s_{i + 1}$ is exactly those remaining characters from 1., let this set be $\mathbb{P}$, then first $|\mathbb{P}|$ characters of $s_i$ should also be $\mathbb{P}$.

**Main Observation.** The character set constraint on prefix of a string can be propagate to previous string, by the similar argument we did to obtain 2.

Then we can propagate all constraint to $s_1$ and solve the whole problem.

Note. lot of string problems have something to do with propagation of equality?
