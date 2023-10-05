This operator is used to decide between two values/expressions resulting the same type based on a condition.

There are different ways to use it in different languages. But for now we'll focus on it's syntax in `C/C++`. Here,
```c
// if the condition is true then it is evaluated as val1 otherwise val2 and we can instead use expressions in place of values given we are careful with the syntax
condition?val1:val2;
```

> [!example]+ Examples
> ```c
> int z;
> // code to get a value in z from somewhere
> int is_z_even = ((z%2)==1)?1:0;
> ```
