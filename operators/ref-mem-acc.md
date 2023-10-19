Now we are jumping to some special stuff people, remember that i mentioned that if we have a variable we can find its address and we can also find the value stored at a given address. Now as we know the task at hand, let's see how it's implemented in C.

- To get the address of a known variable we just place an \& before it and we get it's address. Please be cautious with this and the binary and operation. The type of variable that stores an address is called a pointer and to preserve it's type we want a pointer of that type. And to declare them just add an \* before the name of the pointer.
- To access the location for getting and modifying the value at an address we just write an \* before the address value or the pointer.
	```c
	// making an integer z
	type z=some_val;
	// making an integer pointer and storing the address of z in it
	type *pz=&z;
	// copying the value at address in pz into y
	type y=*pz;
	// modifying the value at the address in pz
	*pz=new_val;
	
	// if we check for the value of z, we'll find that it's now updated to new_val
	```

So you remember that we can create collections of elements as mentioned earlier. But now we want to know the value of a particular element of that collection, how do we do that? Well it depends on what type of collection we are dealing with, an array(or a pointer), a structure, pointer to a structure. Let's cover them one by one.
- Array, the members are the $i^{th}$ elements, done by using the square brackets(\[\])
	```c
	type arr[capacity];
	
	arr[idx]; // fetches the element at index idx (0-based indexing)

	idx[arr]; // also works the same
	```
- Arrays and pointers are alike in terms of member access and they work in this fashion.
	```c
	type* p=arr;
	
	p[idx];
	```
- Structured Collection, elements have names, done using the dot(\.)
	```c
	collection_type collection_name=collection_value;
	
	collection_name.element_name;
	```
- Pointer to a structured collection, now we can either de-reference the address using an asterisk(\*) and dot(\.) or just use an arrow (\-\>)
	```c
	collection_type*collection_ptr=collection_address;
	
	(*collection_ptr).element_name;

	collection_ptr->element_name;
	```