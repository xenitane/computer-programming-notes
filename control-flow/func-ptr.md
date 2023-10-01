The functions we make are also identifiers and they also have a type. So there can also be pointed to right? The way we use function pointers varies from language to language. Here, we'll be using c/c++ and we'll see how it's done.

The way we represent a function pointer is as follows:
```c
(type)(*func)(argument_types_seperated_by_coma)
```

example:
```c
#include<stdio.h>

void exec((int)(*func)(int,int),int x,int y){
	int res=func(x,y);
	printf("%d\n",res);
}

int multiply(int x,int y){
	return x*y;
}

int main(){
	exec(multiply,10,11);
	return 0;
}
```
