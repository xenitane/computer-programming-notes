Now that we are running a program, we want to be able to give input to our program and receive an output from it, right? So for that we need the I/O and in C, it's implementation is below:

- To take input from console, `scanf` and variants
    `scanf(const char* format, address of variables seperated by coma)`
	the `scanf` function returns an integer signifying the number of successful inputs it has read and in case of a mismatch returns `0`.
	[reference](https://en.cppreference.com/w/c/io/fscanf)
- To print output to the console, `printf` and variants
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

The first argument that these functions take is a format string for the input/output. The format string can take string literals to represent different data types and even further how to depict them. A complete list of them will be there in the reference article linked above along with the different variants of these functions.