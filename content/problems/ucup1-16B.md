**Problem.** Given $(n, m, v, a_n)$, consider choosing an arbitrary size $v$ index set $I$ and add $1$ to $a_i$ over all $i \in I$, for $m$ times, find # possible prefix of arg_sort($a_n$). ($n, m, a_i \le 100$)

> [!solving sketch]- solving sketch
> ```text
>
> Fix the bound x:
> 
>   ai >= x -> choose all
>   ai < x -> choose a good subset
> 
>   - exist ai = x after ops
> 
>   subset (contain ai >= x) b is good iff
>     
>     - (bj >= x - m) for all j
>     - (sum(x - bj) over all bj < x) <= v * m
>     - |b| >= v or (sum(x - ak) over all ak not in b) >= (v - |b|) * m
> 
>   if using DP:
> 
>   [n][sum][|b|] -> O(n^2 mv)?
>   - how to gurantee existence of x
> 
>   a set may be counted in multiple x
> 
> 
> - How to decide a valid subset?
> 
>   case 1 (|b| >= v):
> 
>     1. max(c) - min(b) <= m
>     2. |b| * max(c) - sum(bi for bi <= max(c)) <= mv
> 
>     consider DP:
>       
>       [|b|][sum(bi)][max(c)][min(b)]
> 
>       [max(c)] can be obtained from partial result of knapsack
> 
>       enumerate max(c) in decreasing order,
> 
>       - > max(c) -> force in
>       - = max(c) -> force out
>       - [max(c) - m, max(c)] -> arbitrary
>       - otherwise -> force out
> 
>       -> maintain knapsack of a window of item -> O(n^4)
> 
>   case 2 (|b| < v):
>     
>     define ex := (v - |b|) * m
> 
>     1. max(c') - min(b) <= m
> 
>     1. <=> sum(max(0, min(b) + m - ci)) >= (v - |b|) * m
>        <=> |c| * (min(b) + m) - sum(ci) >= (v - |b|) * m
>     
>     - c'i depends on choice of b
> 
>     -> how to compute c'?
>     
>     - c' only depends on sum(c), |c|.
> 
>     enumerate min(b), maintain [|c|][sum(max(0, min(b) + m - ci))]?
> ```
