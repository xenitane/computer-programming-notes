In certain situations we have to execute a piece of code repetitively until a condition is met, we achieve that by using loops and for that purpose we use the `while` and `for` keywords.

The syntax for both is as follows
1. while loop
```c
// this loop will run until the condition remains true
while(condition){
	// write code to do stuff
}
```
2. for loop
```c
// the syntax of this loop allows us to initialize/create some values(optional), then it takes acondition on which it will run similar to the while loop and further we can also mention a propogation statement which executes after the code inside the loop is executed.
// Note that we are using semicolons(;) to seperate the three statements in the for loop.
// The varibles we create in the initialization statement can be accessed in the loop but not outside of it.
for(initialization;condition;propgation){
	// write code to do stuff
}
```

As we have seen that these loops above check if the condition is met first and the start the process, but is there a way to reverse the process to execute some code and then check the condition. That is done using the `do{}while(condition);` loop.

the syntax is as follows:

```c
do{
	// code to be executed
}while(condition);
```