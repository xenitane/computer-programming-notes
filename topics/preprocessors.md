Preprocessors are a part of `C/C++` syntax that are evaluated during compile time and serves various purposes which make programming easier for us. They are generally preceded by a #(hash) symbol.

some examples are below

```c
// these preprocessors copy the contents of the header files in their place
#include<header_file> 
#include "header_file"

// this preprocessors define a macro
// be it standalone or a representative,
// with or without arguments
// and these are valid and accessible
// from the line they are declared until they
// are invalidated using undef
#define MACRO_NAME
#define MACRO_NAME1 optional_value
#define MACRO_NAME2(args)
#define MACRO_NAME3(args) optional_expression

// this preprocessor invalidates any previously
// defined macro
#undef MACRO_NAME

// conditional preprocessors
#if condition
// code
#else
//code
#endif

#if condition
// code
#elif condition2
//code
#endif

// works if the mentioned macro is defined
#if defined(MACRO_NAME)
//code
#endif

// same as above
#ifdef MACRO_NAME
//code
#endif

// works if the mentioned macro is not defined
#ifndef MACRO_NAME
//code
#endif

// and finally we have a preprocessor that guides
// the compiler on how to process certain peices
// of code like optimizations, target processors
/// etc and that's
#pragma GCC optimize(coma seperated optimizations)
// this preprocessor tells the compiler to
// optimize the code during compile time and there
// are many more like this
```

[reference](https://en.cppreference.com/w/c/preprocessor)

some other examples:
```c
#include<stdio.h>

#define MOD 1000000009

#define lli long long int

int main(){
	lli aa=0x100000000LL;
	// same as long long int aa;
	printf("%d\n",MOD);
	printf("%ld\n",aa);
	return 0;
}

#undef MOD
```

```c
#include<stdio.h>

#define sqr(x) (x) * (x)

int main(){
	int a=10;
	int b=sqr(a);
	printf("%d\n",b);
	return 0;
}

#undef sqr
```

```c
#include<stdio.h>

// making a debugger if the macro JELLY is not
// defined otherwise just an empty statement
#ifndef JELLY
#define JELLY
#define deb(x) fprintf(stderr, "%d\n", x)
#else
#define deb(x)
#endif

int main(){
	int x=10;
	deb(x);
	return 0;
}
```