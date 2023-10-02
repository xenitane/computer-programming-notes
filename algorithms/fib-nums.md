We have the famous Fibonacci series which is computed as follows:
$$\begin{align}
F(0)&=0 \\
F(1)&=1 \\
F(n)&=F(n-1)+F(n-2)&\{a>1\}
\end{align}$$
and the series evolves as: $0,1,1,2,3,5,8,13,21,34,55,.....$

Now let's calculate it.

## Naive Approach
Let's just recursive call for the older values and add them:
```pseudo
	\begin{algorithm}
	\caption{$N^{th}$ Fibonacci Term}
	\begin{algorithmic}
		\Procedure{NthFibTerm}{$n$}
			\If{$n<2$}
				\Return $n$
			\Else
				\Return \Call{NthFib}{$n-1$}+\Call{NthFib}{$n-2$}
			\EndIf
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

### Analysis
- Time Complexity:
  Here we're making two subsequent calls in each function so the number of operation grow exponentially.	
  $$\begin{align}
	T(n)&=\begin{cases}
	\Theta(1) & \text{if } n<2\\
	T(n-1)+T(n-2)+\Theta(1)\leq 2*T(n-1)+\Theta (1) & \text{otherwise}
	\end{cases} \\
	&=\Theta(2^n)
	\end{align}$$
- Space Complexity:
  Here at a particular instance we are making $n$ subsequent calls,$\therefore M(n)=O(n)$.
## Instead of calls let's Iterate
in the method above we see that we are making a lot of calls for evaluating previous terms and not even storing them. Let's do that
```pseudo
	\begin{algorithm}
	\caption{$N^{th}$ Fibonacci Term}
	\begin{algorithmic}
		\Procedure{NthFibTerm}{$n$}
			\If{$n<2$}
				\Return $n$
			\EndIf
			\State $data \gets [0,1]$
			\State $i \gets 1$
			\While{$i<n$}
				\State $data.append(data_i+data_{i-1})$
				\State $i \gets i+1$
			\EndWhile
			\Return $data_n$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
### Analysis:
- $M(n)=O(n)$
- $T(n)=\Theta(n)$ cause it's simply one loop

## Save Memory
We can see that even after making the array we just need the last 2 elements, so instead of an array let's work with just 2 variables.
```pseudo
	\begin{algorithm}
	\caption{$N^{th}$ Fibonacci Term}
	\begin{algorithmic}
		\Procedure{NthFibTerm}{$n$}
			\State $a \gets 1$
			\State $b \gets 0$
			\While{$n>0$}
				\State $a \gets a+b$
				\State exchange $a$ with $b$
				\State $n \gets n-1$
			\EndWhile
			\Return $b$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
### Analysis
- $M(n)=O(1)$
- $T(n)=O(n)$

## Here comes fancy math

Let's start by transforming $\begin{bmatrix} F_{n-1}\\F_{n-2}\end{bmatrix}$ to$\begin{bmatrix} F_{n}\\F_{n-1}\end{bmatrix}$. This transformation can be done using a matrix multiplication. Let's see that
$$\begin{align}
\begin{bmatrix}F_{n}\\F_{n-1}\end{bmatrix}&=\begin{bmatrix}F_{n-1}+F_{n-2}\\F_{n-1}\end{bmatrix}  \\
&=F_{n-1}*\begin{bmatrix}1\\1\end{bmatrix}+F_{n-2}*\begin{bmatrix}1\\0\end{bmatrix} \\
&=\begin{bmatrix}1&1\\1&0\end{bmatrix}*\begin{bmatrix}F_{n-1}\\F_{n-2}\end{bmatrix} \\
&=\begin{bmatrix}1&1\\1&0\end{bmatrix}^{n-1}*\begin{bmatrix}F_{1}\\F_{0}\end{bmatrix} \\
&=\begin{bmatrix}1&1\\1&0\end{bmatrix}^{n-1}*\begin{bmatrix}1\\0\end{bmatrix} \\
\end{align}$$
Now all we have to do is raise $\begin{bmatrix}1&1\\1&0\end{bmatrix}$ to power $n-1$ and the top left term of the final matrix will be our answer, let's see how and for ease we'll use the _binary exponentiation[^1]_ method with matrices.

```pseudo
	\begin{algorithm}
	\caption{$N^{th}$ Fibonacci Term}
	\begin{algorithmic}
		\Procedure{NthFibTerm}{$n$}
		\State $base \gets [[1,1],[1,0]]$
		\State $res \gets [[1,0],[0,1]]$
		\State $n \gets n-1$
		\While{$n>0$}
			\If{$n\bmod2==1$}
				\State $res \gets$ \Call{MatMul}{$res,base$}
			\EndIf
			\State $base \gets$ \call{MatMul}{$base,base$}
			\State $n \gets \lfloor\frac{n}{2}\rfloor$
		\EndWhile
		\Return $res_{0,0}$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
### Analysis:
- $M(n)=O(1)$
- $T(n)=O(\log_{2}n)$ from binary exponentiation


[^1]: [binary exponentiation](bin-exp.md)