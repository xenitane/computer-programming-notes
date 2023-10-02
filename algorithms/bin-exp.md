The task we have at hand is to calculate $b^p$ $\{p \in \mathbb{W}\}$, let's get to it.

## Naive Approach
Let's just initialize a variable with 1 and multiply it by $b$, $p$ times.
```pseudo
	\begin{algorithm}
	\caption{Exponentiation}
	\begin{algorithmic}
		\Procedure{Exp}{$b,p$}
			\State $res \gets 1$
			\For{$i \gets 1$ \To $p$}
				\State $res \gets res*b$
			\EndFor
			\Return $res$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
### Analysis
- $M(n)=O(1)$
- $T(n)=O(n)$

## Math Incoming
Let's rewrite $p$ as $p=2*\lfloor\frac{p}{2}\rfloor+(p\bmod2)$,
$$\begin{align}
b^p&=b^{2*\lfloor\frac{p}{2}\rfloor+(p\bmod2)} \\
&=(b^{\lfloor\frac{p}{2}\rfloor})^{2}*b^{p\bmod2}
\end{align}$$
depending on the value of $p\bmod2$, $b^{p\bmod2}$ can either be $b$ or $1$ and $b^{\lfloor\frac{p}{2}\rfloor}$ can be evaluated by recalling this method.

```pseudo
	\begin{algorithm}
	\caption{Exponentiation Binary Recursive}
	\begin{algorithmic}
		\Procedure{BinExp}{b,p}
			\State $res \gets$ \Call{BinExp}{$b,\lfloor\frac{p}{2}\rfloor$}
			\State $res \gets res*res$
			\If{$p\bmod2==1$}
				\State $res \gets res*b$
			\Endif
			\Return $res$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
### Analysis
- Time Complexity:
  $$\begin{align}
	T(n)&=\begin{cases}
	\Theta(1) & \text{if } n<1\\
	T(\lfloor\frac{n}{2}\rfloor)+\Theta(1) & \text{otherwise}
	\end{cases} \\
	&=\Theta(\log_{2}(n))
	\end{align}$$
- Space Complexity:
  The function call stack goes to a depth same as the time complexity, $\therefore M(n)=\Theta(\log_{2}(n))$.

> [!tip] Can we turn the above situation into a iterative one instead of recursive one. Yes we can.

Let's revisit the _number systems[^1]_, now represent $p$ in binary.
$$\begin{align}
p&=(p_{n}p_{n-1}p_{n-1}\dots p_{2}p_{1}p_{0}) \\
&=\sum_{i=0}^{n}p_{i}2^i \\
\implies b^p&=b^{\sum^{n}_{i=0}p_{i}2^i} \\
&=\prod^{n}_{i=0}b^{p_{i}2^i}
\end{align}$$
And depending on the value of $p_{i}$ the $i^{th}$ term will either be $1$ or $b^{2^i}$ and $b^{2^i}=(b^{2^{i-1}})^2$ $\forall i$. Using these findings we can proceed as
```pseudo
	\begin{algorithm}
	\caption{Exponentiation Binary Iterative}
	\begin{algorithmic}
		\Procedure{BinExp}{$b,p$}
			\State $res \gets 1$
			\While{$p>0$}
				\If{$p \bmod 2 == 1$}
					\State $res \gets res*b$
				\EndIf
				\State $b \gets b*b$
				\State $p \gets \lfloor\frac{p}{2}\rfloor$
			\EndWhile
			\Return $res$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
### Analysis
- $M(n)=O(1)$
- $T(n)=O(\log_{2}(n))$