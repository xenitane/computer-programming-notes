These operators are used to compare to values. And these are the comparative operators we have:
1. **\=\=** : Equals - checks if the values on both it's sized are exactly equal
2. **!\=** : Not Equals - the opposite of equals operation, i.e. checks if the operands it received are unequal
3. **<** : Less Than - checks if the value of the left operand is less than that of the one on the right
4. **<=** : Less Than Or Equal To - checks if the value of the left operand is less than or equal to that of the one on the right
5. **>** : Greater Than - checks if the value of the left operand is greater than that of the one on the right
6. **>=** : Greater Than Or Equal To - checks if the value of the left operand is greater than or equal to that of the one on the right

## Examples
```c
int a=5, b=3, c=5, d=7;

a==c   // true
a!=b   // true
a>b    // true
a>=c   // true
a<d    // true
b<=c   // true  
```

> [!note] A new comparison operator is now added in `C++` starting from the `C++20` standard called the three way comparison operator written as `<=>`.
> ```cpp
> a<=>b;
> /*
> is negative when a is less than b
> is zero when a is equal to b
> is positive when a is greater than b
> */
> 
> 10<=>10; // 0
> 1<=>2;   // -ve
> 2<=>1;   // +ve
> ```