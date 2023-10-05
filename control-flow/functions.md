suppose we have a type of task we want to perform multiple times in our code at different places, what is better, writing code for it again and again or writing it once and using it at those necessary places in just one line.
well functions/methods are just the tool for that task. they take in information and do a task and supply back or `return` a result value(optional too) to us.

general outline for a function in c
```c
/*
function_type function_name(arguments){
	function body
	return result(if required)
}
*/
int my_func(int x){
	// do something
	return result;
}

void my_func2(){
	// do somethings
}

```

Every function type except void returns a value of the type of the function.

In C we pass arguments by value, hence if we are using structure, a copy of it will be passed to the function, not the original object. And that copy will be stored in the function call stack and when the function exits, that memory is freed.

Functions are also variables which can be passed into other functions and to do that we use [[func-ptr.md|function pointer]].

> [!info] for a void function the return keyword does not need a value, just `return;` is sufficient to exit the function.
