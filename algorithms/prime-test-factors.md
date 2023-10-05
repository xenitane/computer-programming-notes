Hey people, it's time for one of the most important tools of maths, the prime numbers. They are natural numbers with only 2 factors. They server various application. So it's important to identify them.

## Prime Test

### Naive Approach
The most basic idea is that we go from $2$ to $n-1$ where $n$ is the number in question and see if it's divisible by anyone, if yes it is composite otherwise prime.

```pseudo
	\begin{algorithm}
	\caption{Prime Test}
	\begin{algorithmic}
		\Procedure{PrimeTest}{$n$}
			\If{$n<2$}
				\Return \FALSE
			\Endif
			\For{$i \gets 2$ \To $n-1$}
				\If{$n \bmod i == 0$}
					\Return \FALSE
				\Endif
			\EndFor
			\Return \TRUE
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

#### Analysis
- $T(n)=O(n-2)=O(n)$
- $M(n)=O(1)$

### Some Improvement

Let's see what we can do to make the code a bit faster, we can surely divide $n$ by a number and still maintain the correctness, but what can it be, let's try $2$. If a number is greater than $\frac{n}{2}$, then on dividing $n$ by it will always be something between $1$ and $2$, hence they are of no need to us in the prime test. So our method changes to.

```pseudo
	\begin{algorithm}
	\caption{Prime Test}
	\begin{algorithmic}
		\Procedure{PrimeTest}{$n$}
			\If{$n<2$}
				\Return \FALSE
			\Endif
			\For{$i \gets 2$ \To $\lfloor\frac{n}{2}\rfloor$}
				\If{$n \bmod i == 0$}
					\Return \FALSE
				\Endif
			\EndFor
			\Return \TRUE
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

#### Analysis
- $T(n)=O\left( \frac{n}{2} \right)=O(n)$
- $M(n)=O(1)$

### Math Incoming
Let's recall the special property of prime number, only 2 factors. This means that composite numbers have more than 2 factors. $\therefore$ if a composite number $n$ has a factor $f$ then $\frac{n}{f}$  is also a factor for the number. And if we consider $f$ the smaller one, then:
$$\begin{align}
f&\leq \frac{n}{f} \\
f^2&\leq n \\
f&\leq \sqrt{ n } \\
\end{align}$$
And we can see that if a number is composite, it will always have a factor less than or equal to it's square root which is greater than one. And this turns our method to:

```pseudo
	\begin{algorithm}
	\caption{Prime Test}
	\begin{algorithmic}
		\Procedure{PrimeTest}{$n$}
			\If{$n<2$}
				\Return \FALSE
			\Endif
			\State $i \gets 2$
			\While{$i*i \leq n$}
				\If{$n \bmod i == 0$}
					\Return \FALSE 
				\EndIf
			\EndWhile
			\Return \TRUE
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

#### Analysis
- $T(n)=O(\sqrt{ n })$
- $M(n)=O(1)$
