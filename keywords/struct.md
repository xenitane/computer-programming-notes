We mentioned making collections of variables to make custom data types of our own requirement and to do that we use the `struct` keyword and we do that as follows:

```c
struct {
	// contents of the structure
} aa; // anonymous struct with single instance aa

struct name_1 {
	// contents of the structure
}; // struct with a name

typedef struct name_1 myStruct1;

//usage

struct name_1 var1;
myStruct1 var2;

typedef struct {
	// content of the structure
}name_2;
// anonymous struct given a name using typedef

//usage
name_2 var3;
```

we can use structs inside each other

```c
typedef struct{
	int x;
}s1;

typedef struct{
	char c;
	s1 sss;
}s2;
```

We have the _primitive data types[^1]_ and we can use them in a special way, bit fields inside a struct where they have to be smaller than their original size, otherwise there will be an compilation error.

```c
typedef struct{
	int x:6;
	int y:10;
	int z:16;
}aaa;
```