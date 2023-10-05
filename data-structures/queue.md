After stacks we gotta learn about queues.

To imagine a stack, imagine a pipe in which you can put stuff from one end at a time and take the stuff out and one a at time too from the opposite end, and the rule is that you can view/pull out the element inserted first.

Below is a visual representation of a queue:
![stack](../diagrams/queue.svg)

And a queue has some properties and functions:
- Properties:
	1. Array for storing the data
	2. Max capacity of the queue
	3. Positions of the front and back element
- Functions:
	1. `push(value)` - inserts the element `value` at the back of the queue
	2. `front()` - supplies us the value at the front element in the stack
	3. `pop()` - remove the front element from the queue
	4. `size()` - tells us how many elements are there in the queue
	5. `empty()` - tells us if the queue is empty.



now let's implement a stack:

```c
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>
#include<assert.h>

typedef struct{
	const long long int MAX_CAPACITY;
	long long int back;
	long long int front;
	int *data;
}queue;

queue* init_queue(long long int);
long long int size(queue*);
void push(queue*,int);
bool empty(queue*);
void pop(queue*);
int front(queue*);
free_queue(queue*);

int main(){
	queue*myQueue=init_queue(10000);
	// now we can do whatever we want with our stack
	free_queue(myQueue);
	return 0;
}

queue* init_queue(long long int MAX_CAP){
	assert(MAX_CAP>=0);
	queue* res=NULL;
	while(res==NULL)
		res=(stack*)calloc(1,sizeof(stack));
	*((int*)&res->MAX_CAPACITY)=MAX_CAP;
	res->back=-1;
	res->front=0;
	res->data=NULL;
	while(res->data==NULL)
		res->data=(int*)calloc(MAX_CAP,sizeof(int));
	return res;
}
// #2196F3
// 33 150 243
long long int size(queue*q){
	long long int sz=q->back-q->front;
	if(sz<0)
		sz+=q->MAX_CAPACITY;
	return sz;
}

void push(queue*q,int val){
	assert(size(q)<q->MAX_CAPACITY);
	q->data[q->back++]=val;
	q->back%=q->MAX_CAPACITY;
}

bool empty(queue*q){
	return q->front==q->back;
}

void pop(queue*q){
	assert(!empty(q));
	q->front=(q->front+1)%s->MAX_CAPACITY;
}

int front(queue*q){
	assert(!empty(q));
	return q->data[q->front];
}

void free_queue(queue*q){
	assert(q!=NULL)
	free(q->data);
	free(q);
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
	long long int back;
	long long int front;
	int *data;
}queue;

queue* init_queue();
long long int size(queue*);
void push(queue*,int);
bool empty(queue*);
void pop(queue*);
int front(queue*);
free_queue(queue*);

int main(){
	queue*myQueue=init_queue();
	// now we can do whatever we want with our stack
	free_queue(myQueue);
	return 0;
}

queue* init_queue(){
	stack* res=NULL;
	while(res==NULL)
		res=(stack*)calloc(1,sizeof(stack));
	res->capacity=1;
	res->back=0;
	res->front=0;
	res->data=NULL;
	while(res->data==NULL)
		res->data=(int*)calloc(1,sizeof(int));
	return res;
}

long long int size(queue*q){
	return q->back-q->front;
}

void push(queue*q,int val){
	q->data[q->back++]=val;
	if(sise(q)==q->capacity){
		long long int ncap=capacity*2;
		int*dres=NULL;
		while(dres==NULL)
			dres=(int*)realloc(q->data,ncap);
		q->capacity=ncap;
		q->data=dres;
	}
}

bool empty(queue*q){
	return q->back==q->front;
}

void pop(queue*q){
	assert(!empty(q));
	q->front++;
	long long int sz=q->front;
	if(sz>1&&sz<=s->capacity/2){
		long long int ncap=q->capacity-sz;
		int*dres=NULL;
		while(dres==NULL)
			dres=(int*)calloc(ncap,sizeof(int));
		for(int i=0;i<ncap;i++)
			dres[i]=q->data[i+sz];
		q->back-=sz, q->front=0;
		free(q->data);
		q->data=dres;
	}
}

int front(queue*q){
	assert(!empty(q));
	return q->data[q->front];
}

void free_queue(queue*q){
	assert(q!=NULL);
	free(q->data);
	free(q);
}
```

> Note: in both pieces of codes above, there are places where you'll see [conditions](../control-flow/conditionality.md), [while loops](../control-flow/loops.md), asserts, temporary [variables](../topics/data-types-vars.md) , [memory management](../topics/memory.md) etc, they are there to make sure the tasks are executed without any issues.
> 
> Try to think what those issues can possibly be.
