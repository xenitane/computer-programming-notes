First and foremost when any program is compiled and executed, the variables, keywords, and a lot of other things are set in a hierarchy and the levels in those are called scopes.

And contrary to popular belief, in this case, the lower hierarchies(scopes) can access the things present in their ancestors but not those in their descendants.

And if we start laying out these hierarchies as they appear, these will be as follows:
1. System Environment or the Operating System
2. The Global Scope of the program
3. The scope of functions we declare in the program
4. The scope we further make inside those functions, and this can be done using _decision statements[^1]_, _loops[^2]_, _switches[^3]_, _functions[^4]_ and a lot of other ways which we'll see later.
5. And subsequently we can create a scope inside a scope by repeating the methods in step 4.


[^1]: [conditionally](../control-flow/conditionality.md)
[^2]:[loops](../control-flow/loops.md)
[^3]: [switch](../control-flow/switch-case.md)
[^4]: [functions](../control-flow/functions.md)
