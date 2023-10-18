After stacks we gotta learn about queues.

To imagine a queue, imagine a pipe in which you can put stuff from one end at a time and take the stuff out and one a at time too from the opposite end, and the rule is that you can view/pull out the element inserted at the earliest.

Below is a visual representation of a queue:
![queue](../diagrams/queue.md)

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
![[../diagrams/operations/fixed-size-queue-functions.md]]
now let's implement a queue:

```c
#ifndef _C_QUEUE_H_
#define _C_QUEUE_H_

typedef struct queue_str {
	const size_t MAX_CAP;
	size_t size;
	size_t front;
	int *data;
} queue_t;
typedef queue_t* queue;

queue create_queue(size_t mcap) {
	queue res = NULL;
	while(!res)
		res = (queue) calloc(1, sizeof(queue_t));
	* (size_t*) & (res->MAX_CAP) = mcap;
	res->front = 0;
	res->size = 0;
	res->data = NULL;
	while(!(res->data))
		res->data = (int*) calloc(mcap, sizeof(int));
	return res;
}

void push(queue q, int val) {
	assert(q->size < q->MAX_CAP);
	q->data[(q->front + q->size) % q->MAX_CAP] = val;
	q->size++;
}

void pop(queue q) {
	assert(q->size > 0);
	q->front = (q->front + 1) % q->MAX_CAP;
	q->size--;
}

int empty(queue q) {
	return q->size == 0;
}

size_t size(queue q) {
	return q->size;
}

int front(queue q) {
	assert(q->size > 0);
	return q->data[q->front];
}

void free_queue(queue q) {
	free(q->data);
	free(q);
}

#endif
```

> [!note] The reason we are using the `assert` function here is to disallow undefined behaviour like trying to pop or view the top value in an empty stack, pushing something in an already full stack. If `assert` receives a zero value or `false` it stops the execution of the program and exits it.

Now there is one more queue where you don't have to worry about the max capacity, would you like to take a look into it.

For this we first need to learn about linked lists as they are going to be essential for making dynamic sized queues. 

Here it goes:

```c
#ifndef _C_QUEUE_H_
#define _C_QUEUE_H_

typedef struct queue_node_str {
	int data;
	struct queue_node_str *next; 
} queue_node_t;
typedef queue_node_t* queue_node;

queue_node create_queue_node(int val) {
	queue_node res = NULL;
	while(!res)
		res = (queue_node) calloc(1, sizeof(queue_node_t));
	res->data = val;
	res->next = NULL;
	return res;
}

typedef struct queue_str {
	queue_node front;
	queue_node back;
	size_t size;
} queue_t;
typedef queue_t* queue;

queue create_queue() {
	queue res = NULL;
	while(!res)
		res = (queue) calloc(1, sizeof(queue_t));
	res->first = NULL;
	res->last = NULL;
	res->size = 0;
	return q;
}

void push(queue q, int val) {
	queue_node qn = create_queue_node(val);
	if(q->first == NULL)
		q->first = qn;
	else
		q->last->next = qn;
	q->last = qn;
	q->size++;
}

void pop(queue q){
	assert(q->front != NULL);
	queue_node tmp = q->front;
	q->front = tmp->next;
	if(q->front == NULL)
		q->back = NULL;
	free(tmp);
	q->size--;
}

size_t size(queue q) {
	return q->size;
}

int front(queue q) {
	assert(q->front != NULL);
	return q->front->data;
}

int empty(queue q){
	return q->size == 0;
}

void free_queue(queue q){
	while(q->front)
		pop(q);
	free(q);
}

#endif
```

> [!note] in both pieces of codes above, there are places where you'll see [conditions](../control-flow/conditionality.md), [while loops](../control-flow/loops.md), asserts, temporary [variables](../topics/data-types-vars.md) , [memory management](../topics/memory.md) etc, they are there to make sure the tasks are executed without any issues.
> 
> Try to think what those issues can possibly be.
