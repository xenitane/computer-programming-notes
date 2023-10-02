What are number but a count for what is in front of us. The most basic way was to just have that many smaller things to denote an equivalence. But soon we ran into a problem, the world has finite resources, and we need to develop a convention to represent these numbers. And that's done by using using special symbols having special meaning under certain restrictions. As all of us are familiar with the symbols for digits and Latin letters, let's proceed further.

Aforementioned number systems are the most common number systems a computer scientist has to use (with character representation starts from `0` to `base-1`):
- binary system: 2 characters needed
  character set: `{0,1}`
- octal system: 8 characters needed
  character set: `{0,1,2,3,4,5,6,7}`
- decimal system: 10 characters needed
  character set: `{0,1,2,3,4,5,6,7,8,9}`
- hexadecimal system: 16 characters needed
  character set: `{0,1,2,3,4,5,6,7,8,9,a,b,c,d,e,f}` (case insensitive)
- base64 system: 65 characters needed
  character set: `{A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z,a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z,0,1,2,3,4,5,6,7,8,9,+,/}`
  >[!info] The 65th character is `=` which is places at the end for padding the data at the ends.

Notation: $(number)_{base}$
examples: $(25)_{10}=(11001)_2=(31)_8=(19)_{16}={Z}_{64}$

So, for any number N in base b, $N=(N_kN_{k-1}\dots N_2N_1N_0)_b\hspace{5mm}\{N_i\in\{0 \dots (b-1)\}\}$. And N is consolidated as $N=\sum^{k}_{i=0}b^i*N_i$.
So to find N<sub>k</sub> for any N in base `b` the expression is: $N_k=\lfloor\frac{(N\bmod b^{k+1})}{b^k}\rfloor$.

To find the representation of a number `N` in base `b` let's do the _complexity analysis[^1]_:

Let's say number of digits in the base `b` representation of `N` are `k`, $k>0, b>1, N\geq 0$ and for no leading zeros, k is smallest and  $\cfrac{N}{b^k}\leq1$  holds true 
$$\implies N\leq b^k \implies log_b(N)\leq k \text{ (applying log on both sides)}$$
$$\text{as }log_b(N)=\frac{log_2(N)}{log_2(b)}=c*log_2(N)\implies k=\Omega(log_2(N))$$

[^1]: [complexity analysis](../topics/complexity.md)