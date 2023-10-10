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
Let's recall the special property of prime number, only 2 factors. This means that composite numbers have more than 2 factors. $\therefore$ if a composite number $n$ has a factor $f$ other than 1 than $\frac{n}{f}$  is also a factor for the number. And if we consider $f$ the smaller one, then:
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

## Sieve for Primes and Smallest Prime Factor
Now that we have seen the test of primes we want to make an array of boolean values denoting if it's index is a prime number and an array for storing the smallest prime factor they have. For this let's take an upper bound of $n$ for the size of these arrays. We'll now initialize a boolean array of size $n+1$ with all values set to true and an integer array of same size with values an an index equal to the index. Now mark the indices $0$ and $1$ in the boolean array as false and in the factor array with $-1$ for notation purposes. Then we'll start from the index $2$ and proceed from thereon. Now just Iterate over the boolean array and see if it's marked as a prime, if yes then go over all it's multiples which are still marked as prime and mark them as composite and fill their smallest prime factor with the prime number you found in the start.

```pseudo
	\begin{algorithm}
	\caption{Sieve And SPF}
	\begin{algorithmic}
		\comment{$ $ declare MAXN as the upper limit for the array}
		\state $is\_prime \gets [$\true,\true,\true$,\dots MAXN+1$ times$]$
		\state $smallest\_prime\_factor \gets [0,0,0,\dots MAXN+1$ times$]$
		\procedure{SieveAndSPF}{}
			\state $is\_prime_{0} \gets$ \false
			\state $is\_prime_{1} \gets$ \false
			\state $smallest\_prime\_factor_{0} \gets$ \false
			\state $smallest\_prime\_factor_{1} \gets$ \false
			\for{$i \gets 2$ \to $MAXN$}
				\if{$is\_prime_{i}==$ \true}
					\state $j \gets i+i$
					\while{$j \leq MAXN$}
						\if{$is\_prime_{j}==$ \true}
							\state $is\_prime_{j} \gets$ \false
							\state $smallest\_prime\_factor_{1} \gets i$
						\endif
						\state $j \gets j+i$
					\endwhile
				\endif
			\endfor
		\endprocedure
	\end{algorithmic}
	\end{algorithm}
```

## Sum and Number of factors
For and given number $n$ we can write is as the product of primes raised to a certain exponent $k$ as $n=\prod_{p \in \mathbb{P}}{p^{k_{p}}}$.
Now the sum of all factors of $n$ including both $1$ and $n$ is given by $SF(n)=\prod_{p \in \mathbb{P}}(\sum_{i=0}^{k_{p}}p^i)$.
And the number of factors of $n$ is given by $\prod_{p \in \mathbb{P}}{(k_{p}+1)}$.

```pseudo
	\begin{algorithm}
	\caption{Sum and Number of factors}
	\begin{algorithmic}
		\procedure{SumNumFac}{$n$}
			\state $sum\_f \gets 1$
			\state $num\_{f}\gets 1$
			\state $p \gets 2$
			\while{$n \geq p*p$}
				\if{$n \bmod p==0$}
					\state $c \gets 1$
					\state $k \gets p$
					\while{$n \bmod p==0$}
						\state $c \gets c+1$
						\state $k \gets k*p$
						\state $n \gets \dfrac{n}{p}$
					\endwhile
					\state $num\_f \gets num\_f*c$
					\state $sum\_f \gets sum\_f*\dfrac{k-1}{p-1}$
				\endif
				\state $p \gets p+1$
			\endwhile
			\if{$n>1$}
				\state $num\_f \gets num\_f*2$
				\state $sum\_f \gets sum\_f*(n+1)$
			\endif
		\EndProcedure 
	\end{algorithmic}
	\end{algorithm}
```

> [!note] This is just the beginning, there are a lot more properties of prime numbers you'll discover along the way and use them.