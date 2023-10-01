Well we have see operators that just need one operand to do an operation but they don't modify the value of the operand, they just produce a result, well here we are with these operators that not only just produce a result but also modify the operand they've received.

And they either do increment or decrement of the operator. And all in all there are 4 of these:

|           | Prefix | Postfix |
| --------- | ------ | ------- |
| Increment | ++x    | x++     |
| Decrement | --x    | x--     |

As we have seen that they either increase or decrease the value of the operand but their position around the operand is what makes them different as that just changes what we'll get out of the expression.

 - Prefix: Here the value of the operand is modified and the result we receive that modified value.
	```c
	int z=12;
	int y=--z;
	// here z will turn 11, and as the value of y receives is the one after the modification is made which is also 11
	
	int a=2;
	int b=a++;
	// here a and b both will be 3 by the logic same as above
	```

- Postfix: Here the value of the operand is modified and the result we receive is a copy of the old value.
	```c
	int z=11;
	int y=z--;
	// here z will turn 10, and as the value of y receives is the copy of the value before the modification is made which is 11
	
	int a=3;
	int b=a++;
	// here a will be 4 and b will be 3 by the logic same as above
	```