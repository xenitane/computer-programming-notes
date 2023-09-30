In C, we have two significant methods for I/O:

- To take input from console
    `scanf(const char* format, address of variables seperated by coma)`
	the `scanf` function returns an integer signifying the number of successful inputs it has read and in case of a mismatch returns `0`.
	[reference](https://en.cppreference.com/w/c/io/fscanf)
- To print output to the console
    `printf(const char* format, values to print seperated by coma)`
    the `printf` function returns the number of characters it has printed to the console.
    [reference](https://en.cppreference.com/w/c/io/fprintf)

## Examples
```c
int a;
int z=scanf("%d",&a);

/*
// the input in the console is 
// let's say a
// in this case z is equal to 0
// let's say 88
// here z will be equal to 1
*/

z=printf("%d\nabc",12); // z will be equal to 6
```

```c
int a=3;
a=printf("%d%d",scanf("%d",&a),a);
printf("%d",a);
/*
Question: predict the output of the above code for the given inputs:
a. hello
b. 81
*/
```

As mentioned above the first argument of these functions is `const char* format` the format for the I/O. The referneces links mentioned above will also provide you with various format specifiers and examples for them.