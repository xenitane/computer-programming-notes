The `inline` keywords is used on functions for making compiler optimization of function inlining. This is similar to macro expansion. Here the function call is replaced with the function body. But there are some caveats you have to make sure of when using it. This make the code a little bit faster at the cost of space. But using it too much can hurt the speed as it consumes too much instruction cache and slows it down.

```c
inline int sum(int a, int b){
	return a+b;
}

int main(){
	int a=53, b=43;
	int z=sum(a, b);
	return 0;
}
```

```c

int main(){
	int a=53, b=43;
	int z=0;
	z=53+43;
	return 0;
}

```