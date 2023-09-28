We have the famous Fibonacci series which is computed as follows:
$$F(0)=0$$
$$F(1)=1$$
$$F(n)=F(n-1)+F(n-2)\hspace{5mm} \{a>1\}$$
and the series evolves as:
$$0,1,1,2,3,5,8,13,21,34,55,.....$$
and to find the nth term using code we have the following approaches along with [complexity analysis](../Topics/index_complexity.md):

- The recursive one:
```
function fibTerm(n: int){
	if n < 2
		return n
	else
		return fibTerm(n - 1) + fibTerm(n - 2)
}
```
Analysis:
$$\begin{equation}T(n)=\left\{\begin{array}{lr}\Theta(1)&\text{if n}<2\\T(n-1)+T(n-2)+\Theta(1)&\text{if n}\geq2\end{array}\right\}\end{equation}$$
$$\implies T(n)=\Theta(2^n)$$

- The iterative one:
```
function fibTerm(n: int){
	initialize a = 1, b = 0
	while n not equals 0
	begin loop
		a = a + b
		swap a and b
		n = n - 1
	end loop
	return b
}
```
Analysis:
$$T(n)=\Theta(n)\text{ cause it's simply one loop}$$

- And now the best method:

Let's transform:
$$\begin{bmatrix}F_i \\ F_{i+1}\end{bmatrix}to\begin{bmatrix}F_{i+1} \\ F_{i+2}\end{bmatrix}=\begin{bmatrix}F_{i+1} \\ F_i+F_{i+1}\end{bmatrix}$$
and here's how we do that:
$$\begin{bmatrix}0 & 1 \\ 1 & 1\end{bmatrix}*\begin{bmatrix}F_{0} \\ F_{1}\end{bmatrix}=\begin{bmatrix}F_{1} \\ F_{0}+F_{1}\end{bmatrix}=\begin{bmatrix}F_{1} \\ F_{2}\end{bmatrix}$$
And for nth term we do:
$$\begin{bmatrix}0 & 1 \\ 1 & 1\end{bmatrix}^n*\begin{bmatrix}F_{0} \\ F_{1}\end{bmatrix}=\begin{bmatrix}0 & 1 \\ 1 & 1\end{bmatrix}^n*\begin{bmatrix}0 \\ 1\end{bmatrix}=\begin{bmatrix}F_{n} \\ F_{n+1}\end{bmatrix}$$
hence F<sub>n</sub> is obtained as:
$$\begin{bmatrix}1 & 0\end{bmatrix}*\begin{bmatrix}F_{n} \\ F_{n+1}\end{bmatrix}=\begin{bmatrix}1 & 0\end{bmatrix}*\begin{bmatrix}0 & 1 \\ 1 & 1\end{bmatrix}^n*\begin{bmatrix}0 \\ 1\end{bmatrix}$$
If we evaluate the above expression we can get the value of the nth Fibonacci term and we are raising the above matrix to a power and guess what [binary exponentiation](../Algorithms/algo_binary_exponentiation.md). And evaluating the above expression the value we obtain is equal to the top-right or bottom-left term of the evaluated matrix in the center(refer properties of symmetric matrices).

```
function mulMat(m1: int[][], m2: int [][]){
	// x is number of rows and y is number of culomns
	initialize x1, y1 = dimensions of m1
	initialize x2, y2 = dimensions of m2
	if y1 not equals x2
		// multiplication is not possible
		return
	initialize resultMat[x1][y2] with 0s
	for i = 0 to x1
	begin loop
		for j = 0 to x2
		begin loop
			for k = 0 to y2
			begin loop
				resultMat[i][k]+=m1[i][j]*m2[j][k]
			end loop
		end loop
	end loop
	return resultMat
}

function fibTerm(n: int){
	intialize resultMat=[[1,0],[0,1]]
	initalize baseMat=[[0,1],[1,1]]
	while n not equals 0
	begin loop
		if n is odd
			resultMat=mulMat(resultMat,baseMat)
		baseMat=mulMat(baseMat,baseMat)
		power = power / 2 (floor)
	end loop
	return resultMat[0][1]
}
```
Analysis:
$$T(n)=\Theta(log_2(n))\text{ from binary exponentiation}$$

In the above journey you've seen how we transitioned from an exponential solution to a logarithmic one, great progress.

Also, keep note of the matrix multiplication method above, and we'll study a method to even optimise that method later, called the [Strassen’s Matrix Multiplication Algorithm](algo_strassen_mat_mul.md).