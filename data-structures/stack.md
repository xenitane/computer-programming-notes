Now we are gonna take a dive into the world of data structures and we'll start this journey from stacks after arrays.

To imagine a stack, imagine a container in which you can put stuff from one end at a time and also that's the same end from which you take the stuff out and one a at time too and the simple rule is the thing you can take out is the last thing you put in.

Below is a visual representation of a stack:
![stack](../diagrams/stack.svg)

And a stack has some properties and functions:
- Properties:
	1. Array in which data will be stored
	2. Max Capacity(Up-to us)
	3. Position of the topmost element
- Functions:
	1. `push(value)` - inserts the element `value` to the top of the stack
	2. `top()` - supplies us the value of the topmost element in the stack
	3. `pop()` - remove the topmost element from the stack
	4. `size()` - tells us how many elements are there in the stack
	5. `empty()` - tells us if the stack is empty.


now let's implement a stack:

```c
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>
#include<assert.h>

typedef struct{
	const long long int MAX_CAPACITY;
	long long int pos;
	int *data;
}stack;

stack*init_stack(long long int);
void push(stack*,int);
void pop(stack*);
bool empty(stack*);
long long int size(stack*);
void free_stack(stack*);


int main(){
	stack*myStack=init_stack(10000);
	// now we can do whatever we want with our stack
	free_stack(myStack);
	return 0;
}

stack* init_stack(long long int MAX_CAP){
	assert(MAX_CAP>=0);
	stack* res=NULL;
	while(!res)
		res=(stack*)calloc(1,sizeof(stack));
	*((int*)&res->MAX_CAPACITY)=MAX_CAP;
	res->pos=-1;
	res->data=NULL;
	while(!res->data)
		res->data=(int*)calloc(MAX_CAP,sizeof(int));
	return res;
}

void push(stack*s,int val){
	assert(s!=NULL);
	assert(s->pos+1<s->MAX_CAPACITY);
	s->data[++(s->pos)]=val;
}

bool empty(stack*s){
	assert(s!=NULL);
	return s->pos<0;
}

void pop(stack*s){
	assert(!empty(s));
	s->pos--;
}

int top(stack*s){
	assert(!empty(s));
	return s->data[s->pos];
}

long long int size(stack*s){
	assert(s!=NULL);
	return s->pos+1;
}

void free_stack(stack*s){
	assert(s!=NULL);
	free(s->data);
	free(s);
}
```

> Note: The reason we are using the `assert` function here is to disallow undefined behaviour like trying to pop or view the top value in an empty stack, pushing something in an already full stack. If `assert` receives a zero value or `false` it stops the execution of the program and exits it.

Now there is one more stack where you don't have to worry about the max capacity, would you like to take a look into it.

Well instead of `MAX_CAPACITY` we just use `capacity` and when we reach that capacity we just double the size of the data array and when we reach below half the capacity we half the size of data array and all this takes is a call to the `realloc` function. [reference](../topics/memory.md)

Here it goes:

```c
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>
#include<assert.h>

typedef struct{
	long long int capacity;
	long long int pos;
	int *data;
}stack;

stack*init_stack();
void push(stack*,int);
void pop(stack*);
bool empty(stack*);
long long int size(stack*);
void free_stack(stack*);

int main(){
	stack*myStack=init_stack();
	// now we can do whatever we want with our stack
	free_stack(myStack);
	return 0;
}

stack* init_stack(){
	stack* res=NULL;
	while(res==NULL)
		res=(stack*)calloc(1,sizeof(stack));
	res->capacity=1;
	res->pos=-1;
	res->data=NULL;
	while(res->data==NULL)
		res->data=(int*)calloc(1,sizeof(int));
	return res;
}

void push(stack*s,int val){
	assert(s!=NULL);
	s->data[++(s->pos)]=val;
	if(s->pos+1==s->capacity){
		long long int ncap=s->capacity*2;
		int *dres=NULL
		while(dres==NULL)
			dres=(int*)realloc(s->data,ncap);
		s->capacity=ncap;
		s->data=dres;
	}
}

bool empty(stack*s){
	return s->pos<0;
}

void pop(stack*s){
	assert(!empty(s));
	s->pos--;
	if(s->pos>=0 && (s.pos+1)*2<=s->capacity){
		long long int ncap=s->capacity/2;
		int *dres=NULL;
		while(dres==NULL)
			dres=(int*)realloc(s->data,ncap);
		s->capacity=ncap;
		s->data=dres;
	}
}

int top(stack*s){
	assert(!empty(s));
	return s->data[s->pos];
}

long long int size(stack*s){
	return s->pos+1;
}

void free_stack(stack*s){
	assert(s!=null);
	free(s->data);
	free(s);
}
```

> Note: in both pieces of codes above, there are places where you'll see [conditions](../control-flow/conditionality.md), [while loops](../control-flow/loops.md), assertions, temporary [variables](../topics/data-types-vars.md) , [memory management](../topics/memory.md) etc, they are there to make sure the tasks are executed without any issues.
> 
> Try to think what those issues can possibly be.

> Here the implemented stack is a stack of integers, it is up-to us what data type we want to use in the stack, can be anything as per our needs.