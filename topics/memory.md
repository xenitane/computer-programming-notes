An important part of executing a program knowing where it is loaded to execute, in the memory aka the RAM.

And RAM stands for random access memory. to access a value we either use the variable or the address where it is stored in the memory. and the type of variable we use to store that address is called pointer.

the way to use pointers can be found _here[^1]_.

further we can use multi-layered pointer by increasing the number of asterisks before the pointer name like:
```c
type z=1;
type *p=&z;
type **p1=&p;
type ***p2=&p1;
// and so on
```

> [!caution]+ Pointers are dangerous, if you don't know what you are doing, you can lead to problematic behavior. See below example.
> ```c
> float f;
> int z=*(int*)&f;
> ```

Now that we know how to manage memory, we can also do something else with it. We want to make lists of elements and a common name for these lists in programming is array and we have two ways to create an array.

An array is a continuous block of memory divided into same sized segments(usually of the data type we need) internally.

The indexing for the elements in the list start from 0 to signify the gap between the that element the first one.

![[../diagrams/array.md|array]]


We have two different ways in which we can make arrays:
- Static sized arrays:
  These arrays are of fixed size, they can't be resized or freed over the runtime.
  
  The way to declare them is as follows:
  ```c
  type name0[capacity];
  type name1[capacity]={coma_seperated_elements_qty_less_than_or_equal_to_capacity};
  type name2[]={coma_seperated_elements};
  type name3[c1][c2]; // declare a matrix, and add more dimensions to the matrix as you need.
  ```

- Now the arrays whose size we can control over the runtime but first we need to learn about the functions that are written in the standard library which help us do that. These are `malloc`, `calloc`, `realloc` and `free`, refer _here[^2]_.
	- `malloc`: This function takes the number of bytes we need to allocate and return the starting address to a block of memory of that size.
	- `calloc`: This function takes 2 argument. First is number of members and second is the size of 1 element and finally returns starting address for a block of memory with specified number of elements of the given size.
	- `realloc`: This function is used for resizing a dynamically allocated block of memory. This function takes 2 arguments. The first is the starting address of the block and the second is the new size we want for it to have. Finally it returns the starting address of the resized block. The resized block can have a different address than the old block as we might need to move it. And be sure that the data is kept intact.
	  > [!note] While resizing if we specify that the new size of the block is $0$, then the old block will be deallocated and we'll receive a null pointer.
	- `free`: this function is used to deallocate dynamically allocated memory. This function just takes the starting address of the memory block.
	  
	```c
	type *name4=(type*)malloc(number_of_bytes);
	type *name5=(type*)calloc(length,sizeof(type));
	name4=(type*)realloc(name4,newsize);
	free(name4);
	realloc(name5,0);
	```

At any moment we can access any element of an array given we know the starting address of the array and the index of the element.

And as we saw that arrays and pointers are similar in how the $i^{th}$ element is accessed. Let's see more on that.
```c
// there is an array arr
arr[idx]; // one way to access the element at index idx
*(arr+idx); // same as above, as we add something to a pointer, the compiler doesn't interpret as how many bytes ahead but as how many element ahead.
```

> [!caution]+ And as arrays are just block in memory which we are accessing directly we can also access element that lie outside of the allocated size cause again just memory addresses are being used here.
> ```c
> int arr[2];
> arr[2]=12; // this lies outside of the block we allocated for the array
> ```



[^1]: [Reference](../operators/ref-mem-acc)
[^2]: https://en.cppreference.com/w/c/memory