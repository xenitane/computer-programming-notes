To navigate to different places in code we also have one more thing called labels and the `goto` keyword. And the way we use it as follows:

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
int i=0;
if(!(i<n))goto loop1_end
loop1:
//code
i=i+1;
if(i<n) goto loop1;
loop1_end:
```
