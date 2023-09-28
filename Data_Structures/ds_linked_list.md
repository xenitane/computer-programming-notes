Now we have an interesting contender to see, the linked lists, suppose, you want to store an sequence of data, but continuous memory of that size is not available, hence we cannot make an [array](ds_array) for this purpose, but there is something else we can do, suppose we created a single block storing one element and also the address where the next element is store in a similar way, and now we have a linked list.

A visual representation for linked-list is given below:
![](../Diagrams/linked_list.svg)

What are some properties and functions for linked list node:
- Properties
	1. the data it holds
	2. address of other node(s)
- Functions:
	1. `insert_after_end`
	2. `insert_before_first`
	3. `search_element`
	4. `delete_element`
	5. etc as per our needs.

Now let's implement them:

```c
#include<stdio.h>
#include<stdlib.h>
#include<assert.h>
#include<stdbool.h>

struct list_node{
	int data;
	struct list_node* next;
};

typedef struct list_node listNode;

listNode* create_node(){
	listNode* res=NULL;
	while(!res)
		res=(listNode*)calloc(1,sizeof(listNode));
	res->data=0;
	res->next=NULL;
	return res;
}

void delete_node(listNode* node){
	free(node);
}

void insert_before_first(listNode**head,int val){
	assert(head!=NULL);
	listNode* mynode=createNode();
	mynode->data=val, mynode->next=*head;
	*head=mynode;
}

void insert_after_end(listnode**head,int val){
	assert(head!=NULL);
	listNode* mynode=createNode();
	mynode->data=val, mynode->next=NULL;
	if(*head==NULL)*head=mynode;
	else{
		listNode* tmp = *head;
		while(tmp!=NULL && tmp->next!=NULL)tmp=tmp->next;
		tmp->next=mynode;
	}
}

listNode* search_element(listNode*head,int val){
	while(head!=NULL){
		if(head->data==val)return head;
		head=head->next;
	}
	retutn NULL;
}

bool delete_element(listnode**head,int val){
	// tbd
}

int main(){
	return 0;
}
```