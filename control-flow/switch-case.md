So far we have seen decision making through _if/else[^1]_ but is there an other efficient way of doing this when we only have to check for the value of a single value/expression. 

And to do that we use the `switch` and `case` keywords, and the way of using that is as follows:

```c
switch(value){
case val1:
	// code1
	break;
case val2:case val3:
	// code2
case val4:
	// code3
	break;
/*
.
. other cases
.
*/
default:
	// code_def
	break;
}
```

The switch statement checks the first case which matched the value passed into it, and starts to execute the code.

And the reason we used the `break` keyword is to exit the switch otherwise it will just fall through to the next pieces of code ignoring the case labels like it will do with cases of `val2`, `val3` in the above example. Hence when `value == val2` or `value == val3` the pieces of code written in place of `//code2`  will be executed and then `//code3` will be executed.

[^1]: [conditionality](conditionality.md)