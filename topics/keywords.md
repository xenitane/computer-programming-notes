In every language there is a basic vocabulary, and for programming languages there are some words for specific functions and they are reserved. Here we’ll study the keywords that are present in the C-language.

`class:multi-col-list`

- `auto`
  The auto specifier is only allowed for objects declared at block scope (except function parameter lists). It indicates automatic storage duration and no linkage, which are the defaults for these kinds of declarations
- `break`
  Causes the enclosing `for`, `while` or `do-while` loop or `switch` statement to terminate
- `case`
  for declaration of the case labels in `switch`
- `char`
  Type specifier for the character types
- `const`
  Type qualifier for constant objects
- `continue`
  Causes the remaining portion of the enclosing `for`, `while` or `do-while` loop body to be skipped
- `default`
  For the declaration of the default label in the `switch` statement
- `do`
  For the declaration of the `do-while` loop
- `double`
  Type specifier for the double precision floating point numbers
- `else`
  For declaration of the alternate branch of the `if` statement
- `enum`
  For declaring the ennumerated type
- `extern`
  The extern specifier specifies `static` storage duration and external linkage. It can be used with function and object declarations in both file and block scope
- `float`
  Type specifier for the single precision floating point numbers
- `for`
  For the declaration of the `for` loop
- `goto`
  Transfers control unconditionally to the desired location
- `if`
  Used where code needs to be executed only if some condition is true
- `inline`
  The intent of the inline specifier is to serve as a hint for the compiler to perform optimizations, such as function inlining, which usually require the definition of a function to be visible at the call site
- `int`
  Type specifier for integer types
- `long`
  Type specifier for long type
- `register`
  The register specifier is only allowed for objects declared at block scope, including function parameter lists. It indicates automatic storage duration and no linkage, but additionally hints the optimizer to store the value of this variable in a CPU register if possible
- `restrict`
  Restrict semantics apply to lvalue expressions only; for example, a cast to restrict-qualified pointer or a function call returning a restrict-qualified pointer are not lvalues and the qualifier has no effect.
  During each execution of a block in which a restricted pointer `P` is declared, if some object that is accessible through `P` is modified, by any means, then all accesses to that object in that block must occur through `P`, otherwise the behavior is undefined
- `return`
  Terminates current function and returns specified value to the caller function
- `short`
  Type specifier for short type
- `signed`
  Type modifier for signed values
- `sizeof`
  Queries size of the object or type in bytes
- `static`
   The static specifier specifies both static storage duration and internal linkage
- `struct`
   For declaration of type consisting of a sequence of members whose storage is allocated in an ordered sequence
- `switch`
   For the declaration of a `switch` statement 
- `typedef`
  The typedef declaration provides a way to declare an identifier as a type alias, to be used to replace a possibly complex type name
- `union`
  A union is a type consisting of a sequence of members whose storage overlaps
- `unsigned`
  Type modifier for unsigned type
- `void`
  For incomplete types and for functions that don’t return a value
- `volatile`
  Every access made through an lvalue expression of volatile-qualified type is considered an observable side effect for the purpose of optimization and is evaluated strictly according to the rules of the abstract machine
- `while`
  For declaration of the `while` and `do-while` loop

[refernece](https://en.cppreference.com/w/c/keyword)