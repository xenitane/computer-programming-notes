two numbers a and b are called multiplicative inverses of each other when,
$$a*b=1\hspace{5mm}\{a,b\hspace{1mm}\epsilon\hspace{1mm}R-\{0\}\}$$
so, for modulo n we write a and b are additive inverses when,
$$a*b\equiv1\mod n\hspace{5mm}\{a,b\in\mathbb{Z}\}$$

suppose we have,
$$\text{prime number }p$$
and
$$a\hspace{2mm}\{a\hspace{1mm}\epsilon\hspace{1mm}N,0<a<p\}$$
then
$$a=(1+1+1 ...1)\text{ a times}$$
$$a^p=(1+1+1 ...1)^p$$
$$a^p=\sum\frac{p!}{\prod^{a}_{i=1}x_i!}\hspace{5mm}\{\sum^a_{i=1}x_i=p,0<=x_i<=p\}$$

let's say x<sub>1</sub> = p, this means all other x<sub>i</sub>(s) will be zero
$$\frac{p!}{p!0!0!...0!}=1$$
and we'll have a such situations where x<sub>i</sub> will be 0, this means
$$a^p=a+p*a*K\hspace{5mm}\{k\in\mathbb{W}\}$$
now divide both sides by a
$$a^{p-1}=1+p*K$$
$$a^{p-1}\equiv1\mod{p}$$
$$a*a^{p-2}\equiv1\mod{p}$$
and as we stated above the situation above says that the multiplicative inverse of a in modulo p is:
$$a^{p-2}$$
and it's general form is:
$$a^{p-2}+k*p\hspace{5mm}\{k\in\mathbb{Z}\}$$
and for large prime numbers like 1000000007 the exponent calculation can take a lot of time, so to speed that up we use the [binary exponentiation method](../../Algorithms/algo_binary_exponentiation.md) with modulo operations.

```
function binExpMod(base: int, power: unsigned int, mod: unsigned int){
	initialize result = 1
	while power not equals 0
	begin loop
		if power is odd
			result = (result * base) % mod
		base = (base * base) % mod
		power = power / 2 (floor)
	end loop
	return result
}

function mulModInv(int a, int p){
	// p is prime
	return binExpMod(a, p-2, p)
}
```

