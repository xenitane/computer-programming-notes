An important part of executing a program knowing where it is loaded to execute, in the memory aka the RAM.

And RAM stands for random access memory. to access a value we either use the variable or the address where it is stored in the memory. and the type of variable we use to store that address is called pointer.

the way to use pointers is as follows:
```c
int z=1;
int *p1=&z; //the & operator when places before a variable gives us its address
// and to access the value at the address in the pointer we dereference it
int k=*p1;
// and similary
*p1=2; // now the value stored in z is 2
printf("%d",z) // the output is 2
```

further we can use multi-layered pointer by increasing the number of asterisks before the pointer name like:
```c
int z=1;
int *p=&z;
int **p1=&p;
int ***p2=&p1;
// and so on
```

And to use a place in memory we usually declare a variable(for single value), array(for continuous block of memory divided in equal size). And sometimes we need to dynamically allocate and deallocate memory, and to do so we use the `malloc`,  `calloc`, `realloc`, `free` and some other functions. [reference](https://en.cppreference.com/w/c/memory)

examples:
```c
// declare an integer variable
int x;

// making an integer array of size 10 and y is also a pointer
int y[10];
// y[i] is same as *(y+i)

// dynamically allocating an integer array of size 20
int *p1=(int*)malloc(20*sizeof(int));
// access using *(p1+5) or p1[5]

// deallocating that memory
free(p1)

// declares an array integer array of size 12 with 0 values i.e. p2[i]=0 for all possible values of i
int *p2=(int*)calloc(12, sizeof(int));

// resize the above array to size 6 and retains first 6 elemets.
p2=(int*)realloc(p2,6*sizeof(int));

// now the memory is freed as array is resized to zero.
p2=(int*)realloc(p2,0);
```

> Pointers are dangerous, if you don't know what you are doing, you can lead to problematic behaviour. See below example.

```c
int z;
float y=*(float*)&z;
```
