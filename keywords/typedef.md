The keyword `typedef` stands for type definitions, and is used for writing type definitions for custom types and also creating aliases, some of you might confuse this with the replacement preprocessor, but i assure you that they are very different. One is for replacement of identifiers and one is for defining types.

It's general syntax goes like:
```c
// for type definitions
typedef definition identifier;
// example
typedef struct {int a, int b, int c} abc;

// for aliasing
typedef existing name identifier;
// example
typedef long long ll;
```

> [!note] Only used for type definitions, can't be used for making short-hands for `else if` or other statements.