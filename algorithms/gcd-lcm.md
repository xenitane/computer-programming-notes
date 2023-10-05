In this article we'll study how the GCD and LCM of two numbers a and b are computed and also the proof of it.

## GCD(greatest common divisor):
The gcd of two numbers $a$ and $b$ is the largest possible natural number that divides both $a$ and $b$, written as $g=\gcd(a,b)$.

In writing, max value $g$ such that $a\mid g, b\mid g$ holds true.

### The Naive Approach
Let's just go through all numbers from $1$ to $\min(a,b)$ and see which largest number divides both.
```pseudo
	\begin{algorithm}
	\caption{GCD Linear}
	\begin{algorithmic}
		\Procedure{GCD}{$a,b$}
			\State $res \gets 1$
			\State $m \gets \min(a,b)$
			\For{$i \gets 1$ \To $m$}
				\If{$a \bmod i==0$ \AND $b \bmod i==0$}
					\State $res \gets i$
				\EndIf
			\EndFor
			\Return $res$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
#### Analysis
- $M(n)=O(1)$
- $T(n)=O(\min(a,b))$

### Time for some fancy math
From Euclid's division lemma[^1], $a=b*q+r$.

We can write:
$$\begin{align}
a&=q_{0}*b+r_{0} \\
b&=q_{1}*r_{0}+r_{1} \\
r_{0}&=q_{2}*r_{1}+r_{2} \\
. \\
. \\
. \\
r_{N-3}&=q_{N-1}*r_{N-2}+r_{N-1} \\
r_{N-2}&=q_{N}*r_{N-1}+0
\end{align}$$

Here we can see that both $a$ and $b$ are divisible by $r_{N-1}$ and since $r_{N-1}$ is a common divisor of $a$ and $b$, $\therefore r_{N-1}\leq g$.
And any number that divides both $a$ and $b$ including $g$ by definition divides $r_{k}$. $\therefore g\leq r_{N-1}$.
By the two statements above we can see that $g=r_{N-1}\implies g=\gcd(a,b)=\gcd(b,a\bmod b)=r_{N-1}$.

```pseudo
	\begin{algorithm}
	\caption{GCD Recursive}
	\begin{algorithmic}
		\Procedure{GCD}{$a,b$}
			\If{$b==0$}
				\Return $a$
			\Else
				\Return \Call{GCD}{$b,a\bmod b$}
			\EndIf
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

```pseudo
	\begin{algorithm}
	\caption{GCD Iterative}
	\begin{algorithmic}
		\Procedure{GCD}{$a,b$}
			\While{$b!=0$}
				\State $a \gets a\bmod b$
				\State exchange $a$ with $b$
			\EndWhile
			\Return $a$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

#### Analysis
Let's take a look at the worst case scenario which comes from the situation where a and b are consecutive _Fibonacci number[^2]_, let's say $a=F_{N+1}$ and $b=F_{N}$. So let's make an iteration table, shall we. And the approximate order of a term in the Fibonacci sequence is given by $N\sim \log_{2}(F_{N})$.

| a         | b         |
| :--------- :| :---------: |
| $F_{N+1}$ | $F_{N}$   |
| $F_{N}$   | $F_{N-1}$ |
| $F_{N-1}$ | $F_{N-2}$ |
| .         | .         |
| .         | .         |
| .         | .         |
| 1         | 0          |
What we saw above was a worst case situation, and in general we observe situations which reach a result in less than $\log_{2}(\min(a,b))$ steps.
$\therefore T(a,b)=O(\log_{2}(\min(a,b)))$.

And as for Space complexity, for the recursive approach it is same as the time complexity and for the iterative one it's constant. Therefore we should prefer the iterative method over recursive ones whenever we can.
> [!note] Further we'll read another version of the GCD Algorithm with an extension which is called the _Extended Euclidean[^3]_ which provides $g=a*x+b*y$.

## LCM(least common multiple):
The lcm of two numbers $a$ and $b$ is the smallest whole number that is divisible by both $a$ and $b$, written as $l=\text{lcm}(a,b)$.

In writing, min value $l$ such that $l\mid a, l\mid b$ hold true.

We can write:
$$\begin{align}
g&=\gcd(a,b) \\
a&=g*f_{a} \\
b&=g*f_{b} \\ \\
\exists l\in\mathbb{Z}, g*l&=a*b \\
\implies g*l&=a*(g*f_{b})=(g*f_{a})*b* \\
\implies l&=a*f_{b}=b*f_{a} \\ \\
\implies &l\mid a\text{, } l\mid b \\ \\
\text{Now }\exists m\in\mathbb{Z^+}&\text{, that is a common multiple of a and b.} \\
\implies \exists f_{1}, f_{2}\text{ such that, }& m=a*f_{1}=b*f_{2} \\
\text{And we also know, }& g=a*x+b*y \\ \\
g*m&=m*(a*x+b*y) \\
&=a*b*x*f_{2}+a*b*y*f_{1} \\
&=a*b*(x*f_{2}+y*f_{1}) \\
&=g*l*(x*f_{2}+y*f_{1}) \\
\implies m&=l*(x*f_{2}+y*f_{1}) \\
\implies m&\mid l \\
\therefore l\text{ divides all possible common multiples}&\text{ of a and b, it must be the smallest among them aka the lcm}
\end{align}$$

```pseudo
	\begin{algorithm}
	\caption{LCM}
	\begin{algorithmic}
		\Procedure{LCM}{$a,b$}
			\Return $(a*b)/$\Call{GCD}{$a,b$} \Comment{use GCD from the above snippets.}
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

[^1]: [euclid division lemma](../number-theory/modulo-arithmetic.md)
[^2]: [Fibonacci Numbers](fib-nums.md)
[^3]: [Extended Euclidean](ext-euclid.md)