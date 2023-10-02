Now that we have seen _decision making[^1]_ and _loops[^2]_, we come to wonder if we have the ability to exit the loops in the middle if certain conditions are met or skip further code.

Well look no further, this is done by the `break` and `continue` keywords.
## break
As the name suggests it is used to exit(break) a loop.
And here is how we use it:
```c
// here we will enter the loop if the condition is true and then the code above the break statement will run and then we'll exit the loop.
while(condition){
	// some code
	break;
	// other code
}

// now this was basic but if we want to do this based on a certain condition we write
while(condition1){
	// code
	if(condition2){
		// code
		break;
	}
	// code
}
```

## continue
as the name suggests this is used to skip over and go to next iteration of the loop.
And here's the syntax:
```c
// here we will enter the loop if the condition is true and then the code above the continue statement will run and then we'll skip over the code below and repeat the process.
while(condition){
	// code
	continue;
	// code
}
// now this was basic but if we want to do this based on a certain condition we write
while(condition1){
	// code
	if(condition2){
		// code
		continue;
	}
	// code
}
```

> [!note] These keywords can also be used in `for` and `do/while` loops.


[^1]: [conditionality](conditionality.md)
[^2]: [loops](loops.md)