This is a special keyword used for determining the size of objects and types in bytes.
## Usage Syntax
```c
size_t sz=sizeof(obj)
```

> [!example]+ Example
> ```c
> typedef struct{
> 	int i;
> 	float f;
> 	char s[4];
> } aa;
> 
> size_t sz=sizeof(aa); // here sz will be 12
> ```