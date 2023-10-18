After queue comes the doubly ended queue also called deque.

To imagine a deque, imagine a pipe in which you can put stuff into and take stuff out from both ends, and the rule is that you can view/pull out the elements that are on the ends of it.

Below is a visual representation of a queue:
![deque](../diagrams/deque.md)

And a queue has some properties and functions:
- Properties:
	1. Array for storing the data
	2. Max capacity of the deque
	3. Positions of the front and back element
- Functions:
	1. `push_back(value)` - inserts the element `value` at the back of the queue
	2. `push_front(value)` - inserts the element `value` at the front of the queue
	3. `front()` - supplies us the value at the front element in the stack without removal
	4. `back()` - supplies us the value at the back element in the stack without removal
	5. `pop_front()` - remove the front element from the queue
	6. `pop_back()` - remove the back element from the queue
	7. `size()` - tells us how many elements are there in the queue
	8. `empty()` - tells us if the queue is empty.

![[../diagrams/operations/fixed-size-deque-functions.md]]
now let's implement a queue:

```c
#ifndef _C_DEQUE_H_
#define _C_DEQUE_H_
typedef struct deque_str {
	const size_t MAX_CAP;
	size_t size;
	size_t front;
	int *data;
} deque_t;
typedef deque_t* deque;

deque create_deque(size_t mcap) {
	deque res = NULL;
	while(!res)
		res = (deque) calloc(1,sizeof(deque_t));
	* (size_t*) & (res->MAX_CAP) = mcap;
	res->size = 0;
	res->front = 0;
	res->back = 0;
	res->data = NULL;
	while(!(res->data))
		res->data = (int*)calloc(mcap,sizeof(int));
	return res;
}

void push_back(deque d, int val) {
	assert(d->size < d->MAX_CAP);
	d->data[(d->front + d->size) % d->MAX_CAP] = val;
	d->size++;
}

void pop_back(deque d) {
	assert(d->size > 0);
	d->size--;
}

int back(deque d) {
	assert(d->size > 0);
	return d->data[(d->front + d->size - 1 + d->MAX_CAP) % d->MAX_CAP];
}

void push_front(deque d, int val) {
	assert(d->size < d->MAX_CAP);
	d->size++;
	d->front = (d->front - 1 + d->MAX_CAP) % d->MAX_CAP;
	d->data[d->front] = val;
}

void pop_front(deque d) {
	assert(d->size > 0);
	d->front = (d->front + 1) % d->MAX_CAP;
	d->size--;
}
int front(deque d) {
	assert(d->size > 0)
	return d->data[d->front];
}

size_t size(deque d) {
	return d->size;
}

int empty(deque d){
	return d->size == 0;
}

void free_deque(deque d) {
	free(d->data);
	free(d);
}

#endif
```

> [!note] The reason we are using the `assert` function here is to disallow undefined behaviour like trying to pop or view the top value in an empty stack, pushing something in an already full stack. If `assert` receives a zero value or `false` it stops the execution of the program and exits it.

Now there is one more deque where you don't have to worry about the max capacity, would you like to take a look into it.

For this we first need to learn about doubly linked lists as they are going to be essential for making dynamic sized queues. 

Here it goes:

```c
#ifndef _C_QUEUE_H_
#define _C_QUEUE_H_

typedef struct deque_node_str {
	int data;
	struct deque_node_str *next;
	struct deque_node_str *prev;
} deque_node_t;
typedef deque_node_t* deque_node;

typedef struct deque_str {
	deque_node front;
	deque_node back;
	size_t size;
} deque_t;
typedef deque_t* deque;

deque_node create_deque_node(int val) {
	deque_node res = NULL;
	while(!res)
		res = (deque_node) calloc(1, sizeof(deque_node_t));
	res->data = val;
	res->next = NULL;
	res->prev = NULL;
	return res;
}

queue create_deque() {
	deque res = NULL;
	while(!res)
		res = (deque) calloc(1, sizeof(deque_t));
	res->first = NULL;
	res->last = NULL;
	res->size = 0;
	return q;
}

void push_back(deque d, int val) {
	deque_node dn = create_deque_node(val);
	if(d->front) {
		d->back->next = dn;
		dn->prev = d->back;
	} else
		d->front = dn;
	d->back = dn;
	d->size++;
}

void pop_back(deque d) {
	assert(d->size > 0);
	deque_node tmp = d->back;
	d->back = d->back->prev;
	if(d->back)
		d->back->next = NULL;
	else
		d->front = NULL;
	free(tmp);
	d->size--;
}

int back(deque d) {
	assert(d->size > 0);
	return d->back->data;
}

void push_front(deque d, int val) {
	deque_node dn = create_deque_node(val);
	if(d->front) {
		d-front->prev = dn;
		dn->next = d->front;
	} else
		d->back=dn;
	d->front=dn;
	d->size++;
}

void pop_front(deque d) {
	assert(d->size  > 0);
	deque_node tmp = d->front;
	d->front = d->front->next;
	if(d->front)
		d->front->prev = NULL;
	else
		d->back = NULL;
	free(tmp);
	d->size--;
}

int front(deque d) {
	assert(d->size > 0);
	return d->front->data;
}

size_t size(deque d) {
	return d->size;
}

int empty(deque d) {
	return d->size == 0;
}

void free_deque(deque d) {
	while(d->back)
		pop_back(d);
	free(d);
}

#endif
```

> [!note] in both pieces of codes above, there are places where you'll see [conditions](../control-flow/conditionality.md), [while loops](../control-flow/loops.md), asserts, temporary [variables](../topics/data-types-vars.md) , [memory management](../topics/memory.md) etc, they are there to make sure the tasks are executed without any issues.
> 
> Try to think what those issues can possibly be.
