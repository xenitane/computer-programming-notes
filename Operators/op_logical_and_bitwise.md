These Operators work with logical operations like we've studied with logic gates till now.

These are the logical operators we have
1. **&&** : And
2. **&** : Bit-wise And
3. **||** : Or
4. **|** : Bit-wise Or
5. **^** : Xor
6. **!** : Not
7. **~** : Bit-wise Not
8. **<<** : Bit-shift to the left
9. **>>** : Bit-shift to the right

## Examples
```c
int a=5, b=12, c=0; // 5 (101), 12 (1100), 0 (0)

a&b    // 4 (100)
a|b    // 13 (1101)
a^b    // 9 (1001)
!a     // 0 (0)
a&&b   // 1 (1)
a&&c   // 0 (0)
c||c   // 0 (0)
a||c   // 1 (1)
~c     // 0xffffffff (considering the size of int is 32 bits)
a<<1   // 10 (1010)
a>>1   // 2 (10)
```
```c

12 //decimal
0b1100 //binary
014 //octal
0xc //hexa
```