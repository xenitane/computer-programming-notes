---
tags:
  - WIP
---
First of all we need Euclid's division lemma and that is presented as this. Given two positive integers `a` and `b`, $a=b*q+r\{a,b\in\mathbb{N}\mid0\leq r<b \mid q\geq 0\}$.
And Further, $r= a\bmod r$.

If `r == 0`, this means a is divisible by b and it is notation is $a\mid b$.
Another notation in this situation that we'll need is, $a \equiv b \bmod{n}\implies a\bmod n=b\bmod n$.

Now let's take a dive into the world of modulo n.now as we go above `n-1`, 
like n, n+1 etc we'll just loop back to 0, 1, 2

![[../diagrams/modn.md|circle of modulo n]]

Further Topics:
`class:multi-col-list`

- [[additive-inverse.md|Additive Inverse]]
- [[multiplicative-inverse.md|Multiplicative Inverse]]
