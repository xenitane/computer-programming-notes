Suppose we have two non-zero number `a` and `b`, such that $a*b=1$. Then it is said that `a` and `b` are multiplicative inverses of each other

And for modulo `n` only natural number less than n are allowed, and the concept of additive inverses becomes $a*b\equiv1\mod n\hspace{5mm}\{a,b\in\mathbb{Z}-\{0\}\}$.

> [!note] note that for a particular n, multiplicative inverse of all number do not exist.
 
suppose we have $p$ and $a$, such that $p\in\mathbb{P}$ and $0<a\leq p$.
Then we can rewrite $a=(1+1+1\dots1)$ a times.
$$
\begin{align}
\implies a^p&=(1+1+1\dots1)^p \\
&=\sum \frac{p!}{\prod_{i=1}^{a}{x_{i}!}}&\{\sum_{i=0}^{a}{x_i}=p\mid 0\leq x_i\leq p\}
\end{align}
$$
if $x_{1}=p\implies x_{2}=x_{3}=\dots=x_{a}=0\implies \frac{p!}{x_{1}!x_{2}!\dots x_{a}}=\frac{p!}{p!0!0!\dots{0}!}=1$. And we have $a$ such situations in total where $x_{i}=p$. And as $p$ is prime, any number less than it won't divide it. In situations where none of $x_{i}=p$ then, $\frac{p!}{\prod x_{i}}=p*K \{K\in\mathbb{N}\}$, hence $a^p=a+p*K=a+p*a*k\{K,k\in\mathbb{W}\}$ as $(a^p)\mid a$. Therefore,
$$
\begin{align}
&a^{p}&=a+p*a*k&  \\
\implies&a^{p-1}&=1+p*k&\text{ (dividing both sides by }a\text{)} \\
\implies&a^{p-1}&\equiv 1\mod{p}& \\
\implies&a*a^{p-2}&\equiv{1}\mod{p}&
\end{align}
$$

and as we stated above the situation above says that the multiplicative inverse of a in modulo p is $a^{p-2}$. And it's general form is $a^{p-2}+k*p\{k\in\mathbb{Z}\}$.

And for large prime numbers like 1000000007 the exponent calculation can take a lot of time, so to speed that up we use the [binary exponentiation method](../Algorithms/algo_binary_exponentiation.md) with modulo operations.

```pseudo
\begin{algorithm}
\caption{Multiplicative Modulo Inverse}
\begin{algorithmic}
	\Procedure{MulModInv}{$a, p$}
		\State $res \gets 1$
		\State $pow \gets p - 2$
		\While{$pow>0$}
			\If{$pow \% 2 == 1$}
				\State $res \gets (res*a)\%p$
			\EndIf
			\State $a \gets (a*a)\%p$
			\State $pow \gets \lfloor\frac{pow}{2}\rfloor$
		\EndWhile
		\Return $res$
	\EndProcedure
\end{algorithmic}
\end{algorithm} 
```