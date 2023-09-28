converting numbers from one base to another like between decimal, binary, octal, hexadecimal, base64 etc.

- decimal system \[0-9\]
- binary system \[0-1\]
- octal system \[0-7\]
- hexadecimal system \[0-9a-f\] or \[0-9A-F\]

$$\text{Notation }(number)_{base}$$
examples
$$ (25)_{10}=(11001)_2=(31)_8=(19)_{16}$$

for any number N in base b
$$N=(N_kN_{k-1}...N_2N_1N_0)_b\hspace{5mm}\{N_i\in\{0 ... (b-1)\}\}$$
$$\text{to consolidate }N=\sum^{k}_{i=0}b^i*N_i$$
So to find N<sub>k</sub> for any N in base `b` the expression is:
$$N_k=\lfloor\frac{(N\%b^{k+1})}{b^k}\rfloor$$
To find the representation of a number `N` in base `b` let's do the [complexity analysis](../Topics/index_complexity.md):

The number of iterations required is equal to number of digits in the final representation. And that's for the smallest value of `k` when the below expression holds true

$$\frac{N}{b^k}\leq1$$
$$\implies N\leq b^k$$
$$\implies log_b(N)\leq k \text{ (applying log on both sides)}$$
$$log_b(N)=\frac{log_2(N)}{log_2(b)}=c*log_2(N)$$
$$\implies T(N)=\Omega(log_2(N))$$
