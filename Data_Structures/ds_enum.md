Suppose we have to create some labels or tags representing some information for different situations but we are sick of writing that specific information again and again, so we came up with `enum`, also called enumerated data-type and by default they represent integers starting from 0.

You can achieve similar results from using `#define` directive but `enum` makes process easier for multiple labels.

```c
// anonymous enums with single instance, but we can use the enum labels everywhere else
enum {
	// coma seperated labels
} aa;

// enums with a name
enum e1{
	// coma seperated labels
};
typedef enum e1 myEnum1;

typedef enum {
	// coma seperated labels
} e2;

// usage
enum e1 x;
myEnum1 y;
e2 alp;
```

Now time for how these labels work. By default the first label takes the value of `0` and then increases by `1` for each next value. But we can set the value of any label to what we want as we declare them.

```c
enum aa{
	success, failure, terminated
}; // success=0, failure=1, terminated=2

typedef enum{
	red, blue, green=3,purple, grey=blue+green,white=3
} colors;
// red=1, blue=1, green=3, purple=4, grey=4, white=3
```

And for some of you who are wondering, the `bool` values `true` and `false` can be created using `enum`.

```c
typedef enum{false,true}bool;
```
