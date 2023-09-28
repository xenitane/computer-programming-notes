In this article we'll study how the GCD and LCM of two numbers a and b are computed and also the proof of it.

GCD(greatest common divisor) of two numbers a and b is the largest possible natural number that divides both a and b and let's denote it using `g`.
In writing:
$$a|g,\text{ }b|g$$
and from [Euclid's division lemma](../Number_Theory/nt_modulo_arithmetic.md)
$$a=b*q+r$$
now we have two situations ahead of us:
1.  `r = 0`
$$a=b*q$$
$$\implies a|b$$
$$\implies b \text{ is the largest natural number that divides both }a\text{ and }b$$
$$\implies g=gcd(a,b)=b$$
Similarly if `b|a`, then
$$g=gcd(a,b)=a$$

2. `r != 0`
$$a=b*q+r$$
$$\implies a\%g=r\%g=0$$
$$\text{since }g\text{ is the gcd of }a \text{ and }b\text{ and also divides }r$$
$$\implies gcd(a,b)=gcd(b,r)=gcd(b,a\%b)$$

and to implement this in code
1. recursive form
```
function gcd(a: unsigned int, b: unsigned int){
	if(b == 0) return a
	else return gcd(b, a % b)
}
```
2. iterative form
```
function gcd(a: unsigned int, b: unsigned int){
	while b not equals 0
	begin loop
		a = a % b
		swap a and b
	end loop
	return a
}
```

LCM(lowest common multiple) of two number a and b is smallest possible whole number that's divisible by both a and b and let's denote it using `l`
In writing:
$$l|a,\text{ }l|b$$
let's say:
$$a=f_a*g\text{ and }b=f_b*g$$
$$\text{since }gcd(a,b)=g$$
$$\implies gcd(\frac{a}{g},\frac{b}{g})=gcd(f_a,f_b)=1$$
$$\implies f_a\text{ and }f_b\text{ are co-prime}$$
$$\text{let's assume }L=a*b$$
$$\text{now }L\%a=(a*b)\%a=0\text{ and }L\%b=(b*a)\%b=0$$
Here L satisfies the condition `L|a` and `L|b` which is the first requirement for a number to be the LCM of two numbers, now we have to find the smallest number that satisfies these conditions.

For that look below:
$$\exists f\text{ such that }l=lcm(a,b)=\frac{L}{f}=a*\frac{b}{f}=b*\frac{a}{f}$$
$$\text{for }l\text{ to attain the smallest value possible, }$$
$$f\text{ needs to be as large as possible and divide both }a\text{ and }b$$
$$\text{and that value is the gcd of }a\text{ and }b,\text{ i.e. }g$$
$$\implies l=lcm(a,b)=\frac{L}{g}=\frac{a*b}{g}=\frac{a*b}{gcd(a,b)}$$
$$\implies a*b=l*g$$

code to find LCM
```
function lcm(a: unsigned int, b: unsigned int){
	initialize g = gcd(a, b) // refer above code
	return (a * b) / g
}
```

Now you'll ask what the need for all this when we can just run a [loop](../Control_Flow/cf_loops.md) from `i=1 to min(a,b)` and in each step check if it divides both `a` and `b`, well there would be nothing wrong with that but the method above just makes the process more efficient. And you ask by how much, well for that we have to take a look at the worst case scenario which comes from the situation where a and b are consecutive [Fibonacci number](algo_nth_fib_term.md), let's say a=F<sub>n</sub> and b=F<sub>n+1</sub>. So let's make an iteration table, shall we. And the approximate order of a term in the Fibonacci sequence is given by it's log with base 2.

|a|b|
|-|-|
|F<sub>n</sub>|F<sub>n+1</sub>|
|F<sub>n+1</sub>|F<sub>n</sub>|
|F<sub>n</sub>|F<sub>n-1</sub>|
|F<sub>n-1</sub>|F<sub>n-2</sub>|
|.|.|
|.|.|
|1|0|

What we saw above was a worst case situation, and in general we observe situations which reach a result in less than log<sub>2</sub>(min(a,b)) iteration. And the same goes for the method to find the LCM.

$$\implies T(a,b)\leq log_2(min(a,b))$$
$$\implies T(a,b)=O(log_2(min(a,b)))$$

Further we'll read another version of the GCD Algorithm with an extension which is called the [extended euclidean](algo_ext_euclid.md).