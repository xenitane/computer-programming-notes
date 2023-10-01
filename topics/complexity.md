---

---
Complexity Analysis is an important thing to know for a programmer, as it provides insights to the performance of the code they are about to write.

We generally care about two things when writing code, and those are consumption of time and memory.

So it is in out best interests to write code that solves the problem but takes minimum resources namely time and memory.

So we use complexity analysis to compute the resources consumed by our code and do necessary optimizations wherever necessary. And even if we have fast code, we prefer the faster one cause each bit of resource matters and they collect over time and it can cost us a lot of money in the long run.

First and foremost, Notations, let's say we have a function f(x) it's bounds are represented as
$$\begin{align}
\omega(g(n))&\text{ - small omega of g(n)}&\implies&\{f(n):\exists c,n_0>0 \text{ such that }0\leq c*g(n)<f(n)\forall n>n_0\} \\ 
\Omega(f(n))&\text{ - big omega of f(n)}&\implies&\{f(n):\exists c,n_0>0 \text{ such that }0\leq c*g(n)\leq f(n)\forall n>n_0\} \\
o(f(n))&\text{ - small omicron of f(n)}&\implies&\{f(n):\exists c,n_0>0 \text{ such that }0\leq f(n)<c*g(n)\forall n>n_0\} \\
O(f(n))&\text{ - big omicron of f(n)}&\implies&\{f(n):\exists c,n_0>0 \text{ such that }0\leq c*g(n)\leq f(n)\forall n>n_0\} \\
\theta(f(n))&\text{ - small theta of f(n)}&\implies&\{f(n):\exists c_1,c_2,n_0>0 \text{ such that }0\leq c_1*g(n)<f(n)< c_2*g(n)\forall n>n_0\} \\
\Theta(f(n))&\text{ - big theta of f(n)}&\implies&\{f(n):\exists c_1,c_2,n_0>0 \text{ such that }0\leq c_1*g(n)\leq f(n)\leq c_2*g(n)\forall n>n_0\}
\end{align}
$$

And if, $f(n)\text{ is bound by }\Omega(g(n))\text{ and }O(g(n))\implies f(n)\text{ is bound by }\Theta(g(n))$.
Now, simplification: $\Theta(an^2+bn+c)=\Theta(n^2)$

We choose the greatest exponent of `n` for simplification.

- Memory Consumption: The memory consumed during the runtime of code. One variable is constant memory, and we can evaluate the number of variables declared over the runtime for the analysis.

- Time Consumption: The Time consumed during solving a problem. All unary, binary, ternary operations need constant time to be evaluated and if needed we have to evaluate the number of expression and operations evaluated for the analysis.

Steps to evaluate the complexity of a problem:
1. For a problem with direct solution we can just write a simple expression and get the result.
2. The next part is evaluating loops, recursions. Simply the number of iterations or function calls.
3. And if there is subsequent calculation, consider it too.

All these steps above give rise to the Master Theorem, It helps when there are subsequent calculations to be considered which arise from dividing the problem into smaller parts and merging their solutions.

It goes with the expression:
$$\begin{align}
C(n)&=a*C(\frac{n}{b})+\Theta(f(n)) \\
a&:\text{ the number of smaller sized problems} \\
b&:\text{ the factor by which the problem size gets reduced} \\
f(n)&:\begin{array}{lr}\text{the bound for the computation required for dividing} \\ \text{the problem into smaller parts, and merging the results.}\end{array}
\end{align}
$$
[reference](https://www.geeksforgeeks.org/advanced-master-theorem-for-divide-and-conquer-recurrences/)
