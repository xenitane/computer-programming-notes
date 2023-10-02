We are given a list of numbers `arr` of length `n`, and we are asked to find a contiguous segment of the array whose sum is maximum.

In formal terms:
Given `arr`, such that `|arr| = n`, find the maximum possible value $\sum_{i=l}^{r}arr_{i}$ where $1\leq l\leq r\leq n$ by varying `l` and `r`.

## Naive Approach
The first and foremost method we can think of is making all possible segments and calculate their sum and store the maximum sum somewhere and finally that will be our answer.

```pseudo
	\begin{algorithm}
	\caption{Maximum Subarray Sum}
	\begin{algorithmic}
		\Procedure{MaxSubArrSum}{$arr,n$}
			\State $res \gets -\infty$
			\For{$r \gets 0$ \To $n-1$}
				\For{$l \gets 0$ \To $r$}
					\State $s \gets 0$
					\For{$k \gets l$ \To $r$}
						\State $sum \gets sum + arr_k$
					\EndFor
					\State $res \gets \max (res,sum)$
				\EndFor
			\EndFor
			\Return $res$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
### Analysis
- Space Complexity: We only made a limited number of variables for this computation.
  $\therefore M(n)=c=O(1)$ also called constant.
- Time Complexity: We are checking all possible sub-arrays, and a sub-array of length `l` appear `n-l+1` times for a value of `l`.
  $\therefore T(n)=c*\sum_{i=1}^{n}{i*(n-i+1)}=c*\frac{n*(n^2+5)}{6}=O(n^3)$ also called cubic.
## Optimization using prefix array
We can say that $\sum_{i=l}^{r}{arr_{i}}=\sum_{m=0}^{r}{arr_{m}}-\sum_{k=0}^{l-1}{arr_{k}}$. Then what we can do is make an array containing the sums of all the prefixes of array including the empty prefix too. and for a certain prefix we'll see the smallest prefix that lies before it and their difference will be the answer.

```pseudo
	\begin{algorithm}
	\caption{Maximum Subarray Sum}
	\begin{algorithmic}
		\Procedure{MaxSubArrSum}{$arr,n$}
			\State $res \gets -\infty$
			\State $pref\_arr \gets [0]$
			\For{$i \gets 0$ \To $n-1$}
				\State $pref\_arr.append(pref\_arr_i+arr_i)$
			\EndFor
			\For {$r \gets 1$ \To $n$}
				\State $min\_pref \gets \infty$
				\For{$l \gets 0$ \To $r-1$}
					\State $min\_pref \gets \min(min\_pref,pref\_arr_l)$
				\EndFor
				\State $res \gets \max(res,pref\_arr_r-min\_pref)$
			\EndFor
			\Return $res$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

### Analysis
- Space Complexity: We are making a new array of same size as the input array and some extra variables for the procedure.
   $\therefore M(n)=c+n=O(n)$ also called linear.
- Time Complexity: Here we are checking all prefixes for an index, which are `idx+1` for any index `idx`.
  $\therefore T(n)=\sum_{i=1}^{n}{c*(i+1)}=c*\frac{n^2+3*n}{2}=O(n^2)$ also called square.

## Another optimization  by storing the minimum prefix
In the above situation we are finding the smallest prefix array for each value of `r`, instead how about using the principle that $\min(arr_{r},arr{r-1},\dots,arr_{1})=\min(arr_{r},\min(arr_{r-1},\dots,arr_{1}))$. And this can be done bu updating the value of `min_pref` in the first loop itself. And the process becomes.

```pseudo
	\begin{algorithm}
	\caption{Maximum Subarray Sum}
	\begin{algorithmic}
		\Procedure{MaxSubArrSum}{$arr,n$}
			\State $res \gets -\infty$
			\State $pref\_arr \gets [0]$
			\For{$i \gets 0$ \To $n-1$}
				\State $pref\_arr.append(pref\_arr_i+arr_i)$
			\EndFor
			\State $min\_pref \gets -\infty$
			\For{$i \gets 1$ \To $n$}
				\State $min\_pref \gets \min(min\_pref,pref\_arr_{i-1})$
				\State $res \gets \max(res,pref\_arr_i-min\_pref)$
			\EndFor
			\Return $res$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

### Analysis
- Space Complexity: Same as earlier, $O(n)$.
- Time Complexity: All we are doing is just iterating over the two arrays.
  $\therefore T(n)=c*n=O(n)$.

## As we have saved time let's save the space too.
We divided the sub array into the sum of two prefixes, and escaped the calculation of the minimum prefix too, let's do something similar for a prefix too. We get $prefix(arr,i)=arr_{i}+prefix(arr,i-1)\{1<i\leq |arr|\}$. And here we just evaded the need of prefix array.

```pseudo
	\begin{algorithm}
	\caption{Maximum Subarray Sum}
	\begin{algorithmic}
		\Procedure{MaxSumArrSum}{$arr,n$}
			\State $res \gets arr_0$
			\State $curr\_pref \gets arr_0$
			\State $min\_pref \gets 0$
			\For{$i \gets 1$ \To $n-1$}
				\State $min\_pref \gets \min(min\_pref,curr\_pref)$
				\State $curr\_pref \gets curr\_pref+arr_i$
				\State $res \gets \max(res,curr\_pref-min\_pref)$
			\EndFor
			\Return $res$
		\EndProcedure
	\end{algorithmic}
	\end{algorithm}
```

### Analysis
- Space Complexity: We are just making 3 variables throughout the process, $\therefore M(n)=O(1)$.
- Time Complexity: We are just going over the array once, $\therefore T(n)=O(n)$.