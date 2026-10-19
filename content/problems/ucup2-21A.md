**Problem.** Given a string $s$ consist of "ABCD", consider the following operation:

- choose a substring that is rotation of "ABCD", and rotate it arbitrarilly.

Find the number of possible string can be obtained by doing such operation any number of times.

**Solution.**

First consider the transformation $s_i = (s_i - A) \pmod{4}$, and consider algorithm similar to decide whether a bracket sequence is RBS, then a string can be decompose into some single element block and block with $4$ equal elements, and they forms a bracket sequence-like structure.

Let $k$ be the number of non-singular block $s$ have, then one can notice that the set of reachable strings are exactly those obtained by inserting $k$ blocks of $4$ equal elements into the string consist of all singular blocks of $s$, preserving this order.

Then the problem can be rephrased as follows:

- Given a string consist of "0123", consider insert $k$ length $4$ string of equal numbers, find the number of possible result strings.

Consider the case where the given string is empty. A string may be obtained by multiple ways of insertion and numbers are matched differently.

**Avoid Overcounting.**

By consider the only ways to matched different numbers obtained by the stack simulation algorithm, the block decomposition of a string would be well-defined. Only then can we derive a recursion formula to count such blocks.
