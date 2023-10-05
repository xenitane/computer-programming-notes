Let's say that you want to revisit a place in you code while execution is being done, so you would like to name that location in your code and that's done using labels. and how you visit these locations is by using the `goto` statement.

to make a label
```c
label_name:
```

to navigate to it
```c
goto label_name;
```

example of creating a while loop using the above mentioned
```c
if(condition){
	loop_start:
	// code for the loop
	if(condition)goto loop_start;
}
// removing the first if statement will turn the above code into a do/while loop
// and we can similarly implement the continue and break statements.
```

> [!tip] As we have seen the _preprocessors[^1]_, there is a method for us to create a label maker for loop labels. Let's see how it's done, shall we. The reason for this is that with this we can make several loops.
> ```c
> #include<stdio.h>
> 
> #define lbl_lp_s(name) lp_s_##name
> #define lbl_lp_e(name) lp_e_##name
> 
> int main(){
> 	int n=97,i=2;
> 	if(i*i<=n){
> 		lbl_lp_s(prm_tst):
> 		if(n%i++==0)goto lbl_lp_e(prm_tst);
> 		if(i*i<=n)goto lbl_lp_s(prm_tst);
> 		lbl_lp_e(prm_tst):
> 	}
> 	return 0;
> }
> ```

[^1]: [preprocessors](../topics/preprocessors.md)