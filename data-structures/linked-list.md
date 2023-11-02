Now we have an interesting contender to see, the linked lists, suppose, you want to store an sequence of data, but continuous memory of that size is not available, hence we cannot make an _array[^1]_ for this purpose, but there is something else we can do, suppose we created a single block storing one element and also the address(es) of other block(s) where similar things are done, and now we have a linked list.

A visual representation different types of linked-lists is given below:
![linked list](../diagrams/linked-list.md)

Here we just have list nodes that have data and a pointers to other node(s) if they exists. And for our use we need functions, some are listed below:
- `insert_before_head(value)`: inserts a node with data `value` before the first node in the list and it becomes the first element.
- `insert_after_tail(value)`: inserts a node with data `value` after the last node of the list.
- `insert_after(data, value)`: inserts a node with data `value` after a node containing `data` as `data`, if no such node exists, then it is up-to us what we want to do, usually we don't insert it.
- `search(value)`: searches the list for node containing `value` and returns a pointer to it.
- `delete(value)`: deletes a node containing `value` and if not found nothing is done.

Let's see how we'll do this
![[../diagrams/operations/singly-linked-list-functions.md]]

```c
/* Singly Linked Lists */

#ifndef _C_LINKED_LIST_H_
#define _C_LINKED_LIST_H

typedef struct list_node_str{
	int data;
	struct list_node_str *next;
}list_node_t;
typedef list_node_t *list_node;

list_node create_list_node(int val){
	list_node res=NULL;
	while(!res)res=(list_node)calloc(1,list_node_t);
	res->data=val,res->next=NULL;
	return res;
}

typedef struct linked_list_str{
	list_node head;
	list_node tail;
}linked_list_t;
typedef linked_list_t *linked_list;

linked_list create_list(){
	linked_list res=NULL;
	while(!res)res=(linked_list)calloc(1,sizeof(linked_list_t));
	res->head=NULL,res->tail=NULL;
	return res;
}

void insert_before_head(linked_list l, int val){
	list_node ln=create_list_node(val);
	(l->size)&&(ln->next=l->head)||(l->tail=ln),l->head=ln;
}

void insert_after_tail(linked_list l, int val){
	list_node ln=create_list_node(val);
	(l->size)&&(l->tail->next=ln)||(l->head=ln),l->tail=ln;
}

list_node search_node(linked_list l, int val){
	list_node res=l->head;
	while(res){
		if(res->data==val)return res;
		res=res->next;
	}
	return NULL;
}

int insert_after_val(linked_list l, int d, int val){
	list_node p=search_node(l, d);
	if(!p)return 0;
	list_node ln=create_list_node(val);
	ln->next=p->next,p->next=ln,(ln->next)||(l->tail=ln);
	return 1;
}

int delete_node(linked_list l, int val){
	list_node temp=l->head;
	if(!temp)return 0;
	if(temp->data==val){
		l->head=temp->next,(l->head)||(l->tail=NULL);
		free(temp);
		return 1;
	} else {
		while(temp->next){
			if(temp->next->data == val){
				list_node temp_1=temp->next;
				(temp_1->next)||(l->tail=temp),temp->next=temp_1->next;
				free(temp_1);
				return 1;
			}
			temp=temp->next;
		}
		return 0;
	}
}

void free_linked_list(linked_list l){
	list_node a;
	while(l->head){
		a=l->head,l->head=a->next;
		free(a);
	}
	free(l);
}

#endif
```

![[../diagrams/operations/doubly-linked-list-functions.md]]

```c
/* Doubly Linked List */

#ifndef _C_LINKED_LIST_H_
#define _C_LINKED_LIST_H_

typedef struct list_node_str{
	int data;
	struct list_node_str *next;
	struct list_node_str *prev;
}list_node_t;
typedef list_node_t *list_node;

list_node create_list_node(int val){
	list_node res=NULL;
	while(!res)res=(list_node)calloc(1,sizeof(list_node_t));
	res->data=val,res->next=NULL,res->prev=NULL;
	return res;
}

typedef linked_list_str{
	list_node head;
	list_node tail;
}linked_list_t;
typedef linked_list_t *linked_list;

linked_list create_list(){
	linked_list res=NULL;
	while(!res)res=(linked_list)calloc(1,sizeof(linked_list_t));
	res->head=NULL,res->tail=NULL;
	return res;
}

void insert_before_head(linked_list l, int val){
	list_node ln=create_list_node(val);
	(l->size)&&(ln->next=l->next)&&(l->head-prev=ln)||(l->tail=ln),l->head=ln;
}

void insert_after_tail(linked_list l, int val){
	list_node ln = create_list_node(val);
	(l->size)&&(ln->prev=l->tail)&&(l->tail->next=ln)||(l->head=ln),l->tail=ln;
}

list_node search_node(linked_list l, int val){
	list_node res=l->head;
	while(res){
		if(res->data==val)return res;
		res=res->next;
	}
	return NULL;
}

int insert_after_val(linked_list l, int d, int val){
	list_node p=search_node(l,d);
	if(!p)return 0;
	list_node ln=create_list_node(val);
	ln->next=p->next,ln->prev=p,p->next=ln,*(ln->next?&ln->next->prev:&l->tail)=ln;
	return 1;
}

// similarly we can implement insert_before_val

int delete_node(linked_list l, int val){
	list_node p=search_node(l,val);
	if(!p)return 0;
	*(p->next?&p->next->prev:&l->tail)=p->prev,*(p->prev?&p->prev->next:&l->head)=p->next;
	free(p);
	return 1;
}

void free_linked_list(linked_list l){
	list_node a;
	while(l->head){
		a=l->head,l->head=a->next,(l->head)&&(l->head->prev=NULL);
		free(a);
	}
	free(l);
}

#endif
```

```c
/* Circular Singly Linked List */
#ifndef _C_LINKED_LIST_H_
#define _C_LINKED_LIST_H_

typedef struct list_node_str{
	int data;
	struct list_node_str *next;
} list_node_t;
typedef list_node_t* list_node;

list_node create_list_node(int val) {
	list_node res = NULL;
	while(!res)
		res = (list_node) calloc(1, sizeof(list_node_t));
	res->data = val;
	res->next = res;
	return res;
}

typedef struct linked_list_str {
	list_node head;
	list_node tail;
} linked_list_t;
typedef linked_list_t* linked_list;

linked_list create_linked_list() {
	linked_list res = NULL;
	while(!res)
		res = (linked_list) calloc(1, sizeof(linked_list_t));
	res->head = NULL;
	res->tail = NULL;
	return res;
}

void insert_before_head(linked_list l, int val) {
	list_node ln = create_list_node(val);
	l->head = ln;
	if(!l->tail)
		l->tail = ln;
	else
		ln->next  = l->tail->next;
	l->tail->next  = ln;
}

void insert_after_tail(linked_list l, int val) {
	list_node ln = create_list_node(val);
	if(!l->tail)
		l->head = ln;
	else
		l-tail->next = ln;
	ln->next = l->head;
	l->tail = ln;
}

list_node search_node(linked_list l, int val) {
	list_node res = l->head;
	if(!res)
		return NULL;
	do {
		if(res->data == val)
			return res;
		res = res->next;
	} while(res != l->head);
	return NULL;
}

int insert_after_val(linked_list l, int d, int val) {
	list_node p = search_node(l, d);
	if(!p)
		return 0;
	list_node ln = create_list_node(val);
	ln->next = p->next;
	p->next = ln;
	if(p == l->tail)
		l->tail = ln;
	return 1;
}

int delete_node(linked_list l, int val) {
	list_node temp = l->head;
	if(!temp)
		return 0;
	if(temp->data == val) {
		if(l->head == l->tail) {
			l->head = NULL;
			l->tail = NULL;
		} else {
			l->head = temp->next;
			l->tail->next = temp->next;
		}
		free(temp);
		return 1;
	} else {
		while(temp->next != l->head) {
			if(temp->next->data == val) {
				list_node temp_1 = temp->next;
				if(temp_1 == l->tail)
					l->tail = temp;
				temp->next = temp_1->next;
				free(temp_1)
				return 1;
			}
			temp = temp->next;
		}
		return 0;
	}
}

void free_linked_list(linked_list l) {
	list_node a;
	while(l->head) {
		a = l->head;
		if(l->head == l->tail) {
			l->tail = NULL;
			l->head = NULL;
		} else {
			l->head = a->next;
			l->tail->next = a->next;
		}
		free(a);
	}
	free(l);
}

#endif
```

```c
/* Circular Doubly Linked List */
#ifndef _C_LINKED_LIST_H_
#define _C_LINKED_LIST_H_

typedef struct list_node_str {
	int data;
	struct list_node_str *next;
	struct list_node_str *prev;
} list_node_t;
typedef list_node_t* list_node;

list_node create_list_node(int val) {
	list_node res = NULL;
	while(!res)
		res = (list_node) calloc(1, sizeof(list_node_t));
	res->data = val;
	res->next = NULL;
	res->prev = NULL;
	return res;
}

typedef struct linked_list_str {
	list_node head;
	list_node tail;
} linked_list_t;
typedef linked_list_t* linked_list;

linked_list create_linked_list() {
	linked_list res = NULL;
	while(!res)
		res = (linked_list) calloc (1, sizeof(linked_list_t));
	res->head = NULL;
	res->tail = NULL;
	return res;
}

void insert_before_head(linked_list l, int val) {
	list_node ln = create_list_node(val);
	if(!l->head) {
		l->head = ln;
		l->tail = ln;
		ln->next = ln;
		ln->prev = ln;
	} else {
		
	}
}

#endif
```