There are a lot of places in the code where we have to execute different code based on different conditions. To achieve that the `if` and `else` keywords are used.

The syntax for using this decision making keywords is as follows:
```c
if(condition){
	// code to execute when the condition is true
}else{
	// code to execute otherwise
}
```

```c
// here the else block is optional if it is not required
if(condition){
	// code to execute when the condition is true
}
```

```c
// we can also create a ladder for if and else which falls through and if a condition is met once the code for that is executed and we exit that ladder
if(condition1){
	// code to execute when condition1 is true
}else if(condition2){
	// code to execute when condition1 is false but condition2 is true
}else if(condition3){
	// code to execute when neither condition1 nor condition2 is true, but condition3 is true and we can extend this further to however many conditions we want.

/*
.
.
.
*/
}else{
	// the code to be executed when none of the above mentioned conditions come true and this block is optional too if not needed.
}
```
