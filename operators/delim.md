Okay, now that we have defined operations. We want to separate them out, we can consider new line to be a good enough separator but the creators of the c language wanted multiple separators working differently for different situations. In programming these separators are called delimiters. And here are the design choices they made:

- **;** : semi-colon - used to denote the end of a statement.
- **,** : coma - this operator has expressions on both its sides, first it evaluate the one on the left and then discards its value, then evaluates the expression on the right and return its type and value.
- **:** : colon - the only use we need to consider now is that this is used to mark labels, cases in switch, second result for a ternary operation and setting length of bit fields.

```c
statement1;

exp1, exp2, exp3;

label_name:

c?vt:vf;

int z :4;
```