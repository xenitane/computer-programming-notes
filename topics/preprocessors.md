Preprocessors are a part of `C/C++` syntax that are evaluated before main compilation process starts and serves various purposes which make programming easier for us. They are generally preceded by a #(hash) symbol.

A detailed reference for them can be found _here[^1]_

We have a lot of preprocessors in the c language but these are the ones, which concern us the most:
- ## Inclusion: (`#incldue`)
	This preprocessors takes a filename (can be a path) and copies the content of that file in the place where it is mentioned. The filename is a string and is enclosed in either angle brackets (\<filename\>) or double quotes (\"filename\"). There is just a subtle difference in these two methods and that is: angle brackets make the compiler look for the file in the standard library of c, in case of double quotes, the compiler looks for the file's absolute path first and if it is not found there, then it looks for it in the standard library.
	```c
	#include <fname.h> // copying fname.h from the standard library
	#include "path/fname1.h" // first looking for the file from the current folder, if not present looking in the standard library
	```
- ## Replacement: (`#define` and `#undef`)
	This one's a cool one, lets say that throughout the code you have to write something long repetitively and that can't be fulfilled via a function, so you are wondering if there is any way to create an alternate we can make that the compiler recognizes and replaces it's value with what we have to write before compilation. Well we just have the way.
	This preprocessor creates an identifier which it replaces with what we want and if we want, we can make it parametric too, and we can invalidate them later as their need is over. The syntax is:
	```c
	#define identifier optiona_replacement
	#define identifier(params) optional_replacement
	#define identifier(params,...) optional_replacement
	#defien identifier(...) optional_replacement
	#undef identifier
	```
	> [!warning] One identifier cannot be defined again unless it's invalidated first using `#undef`.

- ## Stringification and Concatenation: (`#` and `##`)
	These are used along with replacement preprocessors to turn text directly into a string or concatenate 2 words without turning them into a string.
	The single hash sign turns the text next to it into a string, and the double hashes concatenate the text around them.
- ## Conditionality:
	Now that we know how to include something and define something, we want our compiler to decide on some behavior based on what is included or what is defined etc before it compiles the code, in that case we need conditionality. The list of directives for this is quiet long as there are a lot if things we have to consider, first there are no curly brackets to bound the conditions, so we use another directive to denote the end of conditionality.
	These are the conditional preprocessing directives we have:
	
	`class: multi-col-list`

	- `#if` - takes in a condition and marks the start of conditionality
	- `#endif` - marks the end of conditionality
	- `#else` - start mark for behavior if above conditions are not met
	- `#elif` - equivalent to else if
	- `#ifdef` - equivalent to if defined
	- `#ifndef` - equivalent to if not defined
	- `#elifdef` - else if version of `#ifdef`
	- `#elifndef` - else if version of `#ifndef`

- ## Line: (`#line`)
	This preprocessor directive tells the compiler how to interpret the line number and filename (which is optional) after a certain point.
	```c
	#line line_no "optional_filename"
	```

---
> [!example]+ Examples
> ```c
> #include<stdio.h>
> 
> #define MOD 1000000009
> 
> #define lli long long int
> 
> int main(){
> 	lli aa=0x100000000LL; // expands to -> long long int aa=0x100000000LL;
> 	printf("%d\n",MOD); // expands to -> printf("%d\n",1000000009);
> 	printf("%ld\n",aa);
> 	return 0;
> }
> 
> #undef MOD
> ```
> 
> ```c
> #define elif else if
> ```
> 
> ```c
> #include<stdio.h>
> 
> #define sqr(x) (x) * (x)
> 
> int main(){
> 	int a=10;
> 	int b=sqr(a); // expands to (a) * (a)
> 	printf("%d\n",b);
> 	return 0;
> }
> 
> #undef sqr
> ```
> 
> ```c
> #include<stdio.h>
> 
> // making a debugger if the macro DEBUG is
> // defined otherwise just an empty statement
> #ifdef DEBUG
> #define deb(x) fprintf(stderr, "%d\n", x)
> #else
> #define deb(...)
> #endif
> 
> int main(){
> 	int z=10;
> 	deb(z);
> 	/*
> 	if DEBUG is defined the above statement expande to -> fprintf(stderr, "%d\n", z);
> 	otherwise it expands to nothing and will be just an empty statement
> 	*/
> 	return 0;
> }
> ```
> 
> ```c
> #define show_var_name(var) printf("%s",#var)
> #define merge(a,b) a##b
> 
> int z=10;
> show_var_name(z); // expands to printf("%s","z");
> printf("=%d\n",z);
> 
> int hithere=0;
> printf("%d\n",merge(hi,there)); // expands to printf("%d\n",hithere);
> ```
> 
> Suppose you are making a header file, and you have defined something inside, so if someone accidentally includes it twice, there will be conflict of definitions, to avoid that we use conditionality too.
> ```c
> #ifndef _header_sign_
> #define _header_sign_
> /* below is the code for the header file
> .
> .
> .
> */
> #endif
> ```
> 
> ```c file:test.c
> #include<assert.h>
> #include<stdio.h>
> 
> int main(){
> #line 732 "i_dont_know.c"
> 	assert(1+1==3);
> 	return 0;
> }
> /*
> the output for this code is:
> i_dont_know.c:732: main: Assertion `1 + 1 == 3' failed.
> */
> ```


[^1]: https://en.cppreference.com/w/c/preprocessor