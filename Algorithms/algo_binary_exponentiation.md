$$\text{To calculate }b^p$$
refer [base conversion](../Number_theory/nt_base_conv.md)
$$p = (p_np_{n-1}....p_3p_2p_1p_0)_2\hspace{5mm}\{p_i\in\{0,1\}\}$$
$$\implies p=\sum^{n}_{i=0}{p_i2^i}$$
$$\implies b^p=b^{\sum^{n}_{i=0}{p_i2^i}}$$
$$\implies b^p=\prod^{n}_{i=0}{b^{p_i2^i}}$$
$$\text{further }\begin{equation}b^{p_i2^i}=\left\{\begin{array}{lr}1,&\text{if }p_i=0\\b^{2^i},&\text{if }p_i=1\end{array}\right\}\end{equation}$$
$$\text{and }b^{2^i}=(b^{2^{i-1}})^2$$

Basically what we have to do is check for `i` if the base value needs to be multiplied in the result and do that and further just square the base value for the next iteration of `i`.

so to implement this in code
```
function binExp(base: int, power: unsigned int)
	initialize result = 1
	while power not equals 0
	begin loop
		if power is odd
			result = result * base
		base = base * base
		power = power / 2 (floor)
	end loop
	return result
```

Another way to represent p,
$$p=2*\lfloor\frac{p}{2}\rfloor + p\%2$$
$$\implies b^p=b^{2*\lfloor\frac{p}{2}\rfloor+p\%2}=(b^{\lfloor\frac{p}{2}\rfloor})^2 * b^{p\%2}$$
```
function binExp(base: int, power: unsigned int)
	if power equals 0
		return 1
	else
		initialize result = binExp(base,power/2) (floor)
		result = result * result
		if power is odd
			result = result * base
		return result
```

[Complexity Analysis](../Topics/index_complexity.md):

$$\begin{equation}T(n)=\left\{\begin{array}{lr}\Theta(1)&\text{ if n=0}\\ T(\frac{n}{2})+\Theta(1)&\text{if n>0}\end{array}\right\}\end{equation}$$
$$\implies T(n)=\Theta(log_2(n))$$

for comparison see the graph below

```functionplot
---
title: Evaluating Exponent
xLabel: power
yLabel: no. of iterations
bounds: [0,1000,0,1000]
disableZoom: true
grid: false
---
f(x)=(x)
g(x)=log2(x)
```

- blue line - standard approach
- red line - binary exponentiation
