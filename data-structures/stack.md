Now we are gonna take a dive into the world of data structures and we'll start this journey from stacks after arrays.

To imagine a stack, imagine a container in which you can put stuff from one end at a time and also that's the same end from which you take the stuff out and one a at time too and the simple rule is the thing you can take out is the last thing you put in.

Below is a visual representation of a stack:
![stack](../diagrams/stack.md)

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

a visual for the above functions:
![[../diagrams/operations/fixed-size-stack-functions.md]]

now let's implement a stack:

```c
#ifndef _C_STACK_H_
#define _C_STACK_H_

typedef struct stack_str{
	const size_t MAX_CAP;
	size_t pos;
	int *data;
}stack_t;
typedef stack_t *stack;

stack create_stack(int mcap){
	assert(mcap>0);
	stack res=NULL;
	while(!res)res=(stack)calloc(1,sizeof(stack_t));
	*(int*)&(res->MAX_CAP)=mcap,res->data=NULL,res->pos=0;
	while(!res->data)res->data=(int*)calloc(mcap, sizeof(int));
	return res;
}

void push(stack s, int val){
	assert(s->pos<s->MAX_CAP);
	s->data[s->pos++]=val;
}

void pop(stack s){
	assert(s->pos>0);
	s->pos--;
}

int top(stack s){
	assert(s->pos>0);
	return s->data[s->pos-1];
}

size_t size(stack s){
	return s->pos;
}

int empty(stack s){
	return s->pos==0;
}

void free_stack(stack s){
	free(s->data);
	free(s);
}

#endif
```

> Note: The reason we are using the `assert` function here is to disallow undefined behavior like trying to pop or view the top value in an empty stack, pushing something in an already full stack. If `assert` receives a zero or `false` value it stops the execution of the program and exits it.

Now there is one more stack where you don't have to worry about the max capacity, would you like to take a look into it.

We can just use dynamic arrays to create them, but there's a catch, for expansion and contraction we need to spend a lot of time and in some cases it might not even be possible as memory is not available. So we'll use linked lists.

Here it goes:

```c
#ifndef _C_STACK_H_
#define _C_STACK_H_

typedef struct stack_node_str{
	int data;
	struct stack_node_str *next;
}stack_node_t;
typedef stack_node_t *stack_node;

stack_node create_stack_node(int val){
	stack_node res=NULL;
	while(!res)res=(stack_node)calloc(1,sizeof(stack_node_t));
	res->data=val,res->next=NULL;
	return res;
}

typedef struct stack_str{
	size_t size;
	stack_node top;
}stack_t;
typedef stack_t *stack;

stack create_stack(){
	stack res=NULL;
	while(!res)res=(stack)calloc(1,sizeof(stack_t));
	res->size=NULL,res->top=NULL;
	return res;
}

void push(stack s,int val){
	stack_node temp=create_stack_node(val);
	temp->next=s->top,s->top=temp,s->size++;
}

void pop(stack s){
	assert(s->top!=NULL);
	stack_node temp=s->top;
	s->top=temp->next;
	free(temp);
}

void top(stack s){
	assert(s->top!=NULL);
	return s->top->data;
}

size_t size(stack s){
	return s->size;
}

int empty(stack s){
	return s->size==0;
}

void free_stack(stack s){
	while(s->top!=NULL)pop(s);
	free(s);
}

#endif
```

> Note: in both pieces of codes above, there are places where you'll see [conditions](../control-flow/conditionality.md), [while loops](../control-flow/loops.md), assertions, temporary [variables](../topics/data-types-vars.md) , [memory management](../topics/memory.md) etc, they are there to make sure the tasks are executed without any issues.
> 
> Try to think what those issues can possibly be.

> Here the implemented stack is a stack of integers, it is up-to us what data type we want to use in the stack, can be anything as per our needs.