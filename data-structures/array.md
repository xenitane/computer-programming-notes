An array is a continuous block of memory divided into same sized segments(usually of the data type we need) internally.

We can also interpret them as lists of elements of same type. And the indexing for the elements in the list start from 0 to signify that the gap between the first element the starting address.

So the index represents the number of elements between the first element and that element.

![[../diagrams/array.svg|array]]

We'll be using `C` for this course and we create arrays in c in many ways:
1. static fixed size array:
```c
type name0[capacity];

type name1[]={coma_seperated_elements}
```
2. dynamically using `malloc` and `calloc`:
```c
type* name2=(type*)malloc(capacity*sizeof(type));

type* name3=(type*)calloc(capacity,sizeof(type));
```

> Note: In `C` we can resize and free dynamically created arrays using the `realloc` function, and we can also use the range of `free` functions to free the memory.

At any moment we can access any element from the array given we know the name of array and the element of index.

Now in these scenarios we can access a memory address that's outside the bounds of our array as we are simply using the memory addresses. So while writing code, make sure that you don't do this as it can lead to undefined behaviour.