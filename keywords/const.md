We all are aware of constants in real life, like $\pi$, $e$, $h$, $G$, $\epsilon_{0}$, $\mu_{0}$, $c$ and the list goes on. And we know we can declare variables while programming, but we also face moments when we want those variables to just be constant and not be updated over the course of runtime of the program. so we need a way to tell the compiler that this is the case, for situations like these the keyword `const` was created. It does exactly what we discussed here, it turns variables into constants and their value has to be assigned during their declaration and stays the same throughout unless we do some pointer black-magic.

```c
const int y=12;

y=5; // syntax error
```

```c
int x=something;
const int z=x; // also works
```

> [!caution] The pointer black magic mentioned earlier
> ```c
> const int i=12;
> *(int*)&i=1;
> ```