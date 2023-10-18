Have you ever faced a situation when you want to save some information about something but have no idea what kind of information it will be until you get it on runtime. In those situations we use `union` of many data types in one and use the one which is necessary during the runtime.

We can simply make a struct but this reduces memory consumption.

```c
union{
	// variables
} aa;

union u1{
	// variables
};
typedef union u1 myUnion1;

typedef union{
	// variables
} u2;

union u1 x;
myUnion1 y;
u2 z;
```

```c
typedef union uu_u{
	int x;
	char y;
	float f;
} uu_t;

```

we can use whatever type of data type we want in a `union`.

```c
typedef union uu_u{
	int x;
	char s[4];
}uu_t;


uu var={.x=0x44434241};
printf("%s\n",var.s);
// predict the output
```
