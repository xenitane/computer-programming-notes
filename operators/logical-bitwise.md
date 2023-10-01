These Operators work with logical operations like we've studied with logic gates till now.

These are the logical operators we have
### logical
1. **&&** : logical and - tells us if both the operands are non-zero
2. **||** : logical or - tells us if either one of the operands is non-zero
3. **!** : logical not - this operator just needs a operand on it's right and it turns non-zero values into zero and turns a zero to one.
### binary
> can only be done on integral types
1. **|** : binary or - used only on integral types and it's result is obtained by performing the logical or on each corresponding bit in the operands
2. **&** : binary and - used only on integral types and it's result is obtained by performing the logical and on each corresponding bit in the operands
3. **^** : binary xor - used only on integral types and it's result is obtained by performing the logical xor on each corresponding bit in the operands, and unfortunately there is no logical version of it.
4. **~** : binary not - this operator also needs one operand and is only used on integral operand and it's result is obtained by performing the logical not on each bit of the operand

### shifting:
> can only be done on integral types, the left operand is what to shift and the right operand is by how much. Both must be integral types and the right one must always be non zero.
> And the way we can see how shifting works is like this, as we said that the size of these types is fixed, let's say that there is a frame in which the number is kept like a picture, we are just moving that data around and seeing the result of that, and the excess bits moved around are lost.
1. **<<** : left-shift - the bits are shifted to the left by the specified amount and the new bits that fill the right are zeros.
2. **>>** : right-shift - the bits are shifted to the right by the specified amount and the new bits that fill the left are all same as the leftmost bit

## Examples
```c
int a=5, b=12, c=0; // 5 (101), 12 (1100), 0 (0)

a&b               // 4 (100)
a|b               // 13 (1101)
a^b               // 9 (1001)
!a                // 0 (0)
a&&b              // 1 (1)
a&&c              // 0 (0)
c||c              // 0 (0)
a||c              // 1 (1)
~c                // 0xffffffff (considering the size of int is 32 bits)
a<<1              // 10 (1010)
a>>1              // 2 (10)
0x90000000 >> 2   // 0xe4000000
```

> [!todo] I have written some numbers in a weird format, that's to save some space and time here, but fear not you'll understand once you cover how to represent numbers in different formats.