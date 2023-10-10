Now that we are running a program, we want to be able to give input to our program and receive an output from it, right? So for that we need the I/O and in C, the functions we are going to use for I/O are defined in the `stdio.h` header file, and below is how to use them:

## Input
To take input from console, _`scanf` and variants[^1]_
  All the functions below are used to extract data and feed them into the variables whose address we pass into them. And they return the number of arguments successfully assigned before the first matching or input failure occurs.
1. `scanf(const char*restrict __fmt, addresses_of_variables)`: this function reads data from the `stdin` file and matches it the format string with string literals fed to it and puts the corresponding values into the variables whose address we have entered later in the respective order.
2. `sscanf(const char*restrict __s, const char*restrict __fmt, addresses_of_variables)`: this function is used to read the data from a character array passed as the first argument and the rest is same as `scanf`.
3. `fscanf(FILE*restrict __file, const char*restrict __fmt, addresses_of_variables)`: this function is used to read the content from a file by passing a file pointer and the later argument and behavior is same as `scanf`.

The **format** string consists of

- non-white-space multi-byte characters except %: each such character in the format string consumes exactly one identical character from the input stream, or causes the function to fail if the next character on the stream does not compare equal.
- white-space characters: any single white-space character in the format string consumes all available consecutive white-space characters from the input (determined as if by calling `isspace` in a loop). Note that there is no difference between "\\n", " ", "\\t\\t", or other white-space in the format string.
- conversion specifications. Each conversion specification has the following format:

- introductory **`%`** character.

- (optional) assignment-suppressing character *. If this option is present, the function does not assign the result of the conversion to any receiving argument.

- (optional) integer number (greater than zero) that specifies _maximum field width_, that is, the maximum number of characters that the function is allowed to consume when doing the conversion specified by the current conversion specification. Note that %s and %[ may lead to buffer overflow if the width is not provided.

- (optional) _length modifier_ that specifies the size of the receiving argument, that is, the actual destination type. This affects the conversion accuracy and overflow rules. The default destination type is different for each conversion type (see table below).

- conversion format specifier.

<hr width="80%" style="margin-left:auto;margin-right:auto" >

`class:table-ver-cell`

-tx-
|Conversion specifier | Explanation | Argument Type |||||||||
|Length Modifier –>||hh|h|(none)|l|ll|j|z|t|L|
|:---:|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|%|Matches literal `%`.|N/A|N/A|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|c|Matches a **character** or a sequence of **characters**.<br><br>If a width specifier is used, matches exactly _width_ characters (the argument must be a pointer to an array with sufficient room). Unlike %s and %\[, does not append the null character to the array.|N/A|N/A|_char*_|_wchar_t*_|N/A|N/A|N/A|N/A|N/A|
|s|Matches a sequence of non-whitespace characters (a **string**).<br><br>If width specifier is used, matches up to _width_ or until the first whitespace character, whichever appears first. Always stores a null character in addition to the characters matched (so the argument array must have room for at least _width+1_ characters)|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|\[set\]|Matches a non-empty sequence of character from set of characters.<br><br>If the first character of the set is **`^`**, then all characters not in the set are matched. If the set begins with **`]`** or **`^]`** then the **`]`** character is also included into the set. It is implementation-defined whether the character **`-`** in the non-initial position in the scanset may be indicating a range, as in **`[0-9]`**. If width specifier is used, matches only up to _width_. Always stores a null character in addition to the characters matched (so the argument array must have room for at least _width+1_ characters)|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|d|Matches a **decimal integer**.<br><br>The format of the number is the same as expected by `strtol` with the value 10 for the `base` argument|_signed char*_ or _unsigned char*_|_signed short*_ or _unsigned short*_|_signed int*_ or _unsigned int*_|_signed long*_ or _unsigned long*_|_signed long long*_ or _unsigned long long*_|_intmax_t*_ or _uintmax_t*_|_size_t*_|_ptrdiff_t*_|N/A|
|i|Matches an **integer**.<br><br>The format of the number is the same as expected by _strtol_ with the value ​0​ for the `base` argument (base is determined by the first characters parsed)|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|u|Matches an unsigned **decimal integer**.<br><br>The format of the number is the same as expected by _strtoul_ with the value 10 for the `base` argument.|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|o|Matches an unsigned **octal integer**.<br><br>The format of the number is the same as expected by _strtoul_ with the value 8 for the `base` argument|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|x,X|Matches an unsigned **hexadecimal integer**.<br><br>The format of the number is the same as expected by _strtoul_ with the value 16 for the `base` argument|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|n| Returns the **number of characters read so far**.<br><br>No input is consumed. Does not increment the assignment count. If the specifier has assignment-suppressing operator defined, the behavior is undefined|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|a,A,e,E,<br>f,F,g,G|Matches a **floating-point number**.<br><br>The format of the number is the same as expected by _strtof_|N/A|N/A|_float*_|_double*_|N/A|N/A|N/A|N/A|_long double*_|
|p|Matches implementation defined character sequence defining a **pointer**.<br><br>`printf` family of functions should produce the same sequence using **`%p`** format specifier| N/A|N/A|_void**_|N/A|N/A|N/A|N/A|N/A|N/A|
[Conversion Format Specifier table for `scanf`]


> [!example]+ Examples
> ```c
> #include <stdio.h>
> #include <stddef.h>
> #include <locale.h>
>  
> int main(void) {
>     int i, j;
>     float x, y;
>     char str1[10], str2[4];
>     wchar_t warr[2];
>     setlocale(LC_ALL, "en_US.utf8");
>  
>     char input[] = "25 54.32E-1 Thompson 56789 0123 56ß水";
>     /* parse as follows:
>        %d: an integer
>        %f: a floating-point value
>        %9s: a string of at most 9 non-whitespace characters
>        %2d: two-digit integer (digits 5 and 6)
>        %f:  a floating-point value (digits 7, 8, 9)
>        %*d: an integer which isn't stored anywhere
>        ' ': all consecutive whitespace
>        %3[0-9]: a string of at most 3 decimal digits (digits 5 and 6)
>        %2lc: two wide characters, using multibyte to wide conversion  */
>     int ret = sscanf(input, "%d%f%9s%2d%f%*d %3[0-9]%2lc",
>                      &i, &x, str1, &j, &y, str2, warr);
>  
>     printf("Converted %d fields:\n"
>            "i = %d\n"
>            "x = %f\n"
>            "str1 = %s\n"
>            "j = %d\n"
>            "y = %f\n"
>            "str2 = %s\n"
>            "warr[0] = U+%x\n"
>            "warr[1] = U+%x\n",
>            ret, i, x, str1, j, y, str2, warr[0], warr[1]);
>     return 0;
> }
> ```


---
## Output
To print output to the console, _`printf` and variants[^2]_
  All the functions below are used to put data from the variables we pass into them and feed it into a reservoir as per the usage goes. The return the number of characters they have sent to the output.
1. `printf(const char*restrict __fmt, values_of_variables)`: this function prints data to `stdout` in the specified format and replaces the string literals with the values of variables passed in the respective order.
2. `sprintf(const char*restrict __d, const char*restrict __fmt, values_of_variables)`: prints to the given character buffer in `__d` and the rest is same as `printf`.
3. `snprintf(const char*restrict __d, unsigned long __maxlen, const char*restrict __fmt, values_of_variables)`: this is a small variation of the `sprintf` function. It prints into `__d` up-to only `__maxlen` characters but return the length of complete possible output, it is generally used to determine the size of buffers needed to print certain information.
4. `fprintf(FILE*restrict __file, const char*restrict __fmt, values_of_variables)`: the same as `printf`, the only difference is that it prints to the file specified by the FILE pointer.

The **format** string consists of ordinary byte characters (except **`%`**), which are copied unchanged into the output stream, and conversion specifications. Each conversion specification has the following format:

- introductory **`%`** character.

- (optional) one or more flags that modify the behavior of the conversion:

- **`-`** : the result of the conversion is left-justified within the field (by default it is right-justified).
- **`+`** : the sign of signed conversions is always prepended to the result of the conversion (by default the result is preceded by minus only when it is negative).
- _space_ : if the result of a signed conversion does not start with a sign character, or is empty, space is prepended to the result. It is ignored if `+` flag is present.
- **`#`** : _alternative form_ of the conversion is performed. See the table below for exact effects otherwise the behavior is undefined.
- **`0`** : for integer and floating point number conversions, leading zeros are used to pad the field instead of _space_ characters. For integer numbers it is ignored if the precision is explicitly specified. For other conversions using this flag results in undefined behavior. It is ignored if `-` flag is present.

- (optional) integer value or `*` that specifies minimum field width. The result is padded with _space_ characters (by default), if required, on the left when right-justified, or on the right if left-justified. In the case when `*` is used, the width is specified by an additional argument of type int, which appears before the argument to be converted and the argument supplying precision if one is supplied. If the value of the argument is negative, it results with the `-` flag specified and positive field width (Note: This is the minimum width: The value is never truncated.).

- (optional) **`.`** followed by integer number or **`*`**, or neither that specifies _precision_ of the conversion. In the case when **`*`** is used, the _precision_ is specified by an additional argument of type int, which appears before the argument to be converted, but after the argument supplying minimum field width if one is supplied. If the value of this argument is negative, it is ignored. If neither a number nor **`*`** is used, the precision is taken as zero. See the table below for exact effects of _precision_.

- (optional) _length modifier_ that specifies the size of the argument (in combination with the conversion format specifier, it specifies the type of the corresponding argument).

- conversion format specifier.

<hr width="80%" style="margin-left:auto;margin-right:auto" >

`class:table-ver-cell` 


-tx-
|Conversion specifier | Explanation | Argument Type |||||||||
|Length Modifier –>||hh|h|(none)|l|ll|j|z|t|L|
|:---:|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|%|Writes literal **`%`**. The full conversion specification must be **`%%`**.|N/A|N/A|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|c|Writes a **single character**.<br><br>The argument is first converted to _unsigned char_. If the **l** modifier is used, the argument is first converted to a character string as if by **%ls** with a _wchar_t[2]_ argument.|N/A|N/A|_int_|_wint_t_|N/A|N/A|N/A|N/A|N/A|
|s|Writes a **character string**<br><br>The argument must be a pointer to the initial element of an array of characters. _Precision_ specifies the maximum number of bytes to be written. If _Precision_ is not specified, writes every byte up to and not including the first null terminator. If the **l** specifier is used, the argument must be a pointer to the initial element of an array of wchar_t, which is converted to char array as if by a call to _wcrtomb_ with zero-initialized conversion state.|^^|^^|_char*_|_wchar_t*_|^^|^^|^^|^^|^^|
|d<br>i|Converts a **signed integer** into decimal representation _[-]dddd_.<br><br>_Precision_ specifies the minimum number of digits to appear. The default precision is 1.<br><br>If both the converted value and the precision are ​0​ the conversion results in no characters.|_signed char_|_short_|_int_|_long_|_long long_|_intmax_t_|_signed size_t_|_ptrdiff_t_|N/A|
|o|Converts an **unsigned integer** into octal representation _oooo_.<br>_Precision_ specifies the minimum number of digits to appear. The default precision is 1. If both the converted value and the precision are ​0​ the conversion results in no characters. In the _alternative implementation_ precision is increased if necessary, to write one leading zero. In that case if both the converted value and the precision are ​0​, single ​0​ is written.|_unsigned char_|_unsigned short_|_unsigned int_|_unsigned long_|_unsigned long long_|_uintmax_t_|_size_t_|unsigned version of _ptrdiff_t_|N/A|
|x<br>X|Converts an **unsigned integer** into hexadecimal representation _hhhh_.<br><br>For the **`x`** conversion letters `abcdef` are used. <br>For the **`X`** conversion letters `ABCDEF` are used.<br>_Precision_ specifies the minimum number of digits to appear. The default precision is 1. If both the converted value and the precision are ​0​ the conversion results in no characters. In the _alternative implementation_ **`0x`** or **`0X`** is prefixed to results if the converted value is nonzero.|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|u|Converts an **unsigned integer** into decimal representation _dddd_.<br><br>_Precision_ specifies the minimum number of digits to appear. The default precision is 1. If both the converted value and the precision are ​0​ the conversion results in no characters.|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|f<br>F|Converts **floating-point number** to the decimal notation in the style _[-]ddd.ddd_.<br><br>_Precision_ specifies the exact number of digits to appear after the decimal point character. The default precision is 6. In the _alternative implementation_ decimal point character is written even if no digits follow it. For infinity and not-a-number conversion style see notes.|N/A|N/A|_double_|_double_|N/A|N/A|N/A|N/A|_long double_|
|e<br>E|Converts **floating-point number** to the decimal exponent notation.<br><br>For the **`e`** conversion style _[-]d.ddd_**`e`**_±dd_ is used.<br>For the **`E`** conversion style _[-]d.ddd_**`E`**_±dd_ is used.<br>The exponent contains at least two digits, more digits are used only if necessary. If the value is ​0​, the exponent is also ​0​. _Precision_ specifies the exact number of digits to appear after the decimal point character. The default precision is 6. In the _alternative implementation_ decimal point character is written even if no digits follow it. For infinity and not-a-number conversion style see notes.|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|a<br>A|Converts **floating-point number** to the decimal exponent notation.<br><br>For the **`e`** conversion style _[-]d.ddd_**`e`**_±dd_ is used.<br>For the **`E`** conversion style _[-]d.ddd_**`E`**_±dd_ is used.<br>The exponent contains at least two digits, more digits are used only if necessary. If the value is ​0​, the exponent is also ​0​. _Precision_ specifies the exact number of digits to appear after the decimal point character. The default precision is 6. In the _alternative implementation_ decimal point character is written even if no digits follow it. For infinity and not-a-number conversion style see notes.|^^|^^|^^|^^|^^|^^|^^|^^|^^
|g<br>G|Converts **floating-point number** to decimal or decimal exponent notation depending on the value and the _precision_.<br><br>For the **`g`** conversion style conversion with style **`e`** or **`f`** will be performed.<br>For the **`G`** conversion style conversion with style **`E`** or **`F`** will be performed.<br>Let `P` equal the precision if nonzero, 6 if the precision is not specified, or 1 if the precision is ​0​. Then, if a conversion with style `E` would have an exponent of `X`:<br>- if _P > X ≥ −4_, the conversion is with style **`f`** or **`F`** and precision _P − 1 − X_.<br>- otherwise, the conversion is with style **`e`** or **`E`** and precision _P − 1_.<br>Unless _alternative representation_ is requested the trailing zeros are removed, also the decimal point character is removed if no fractional part is left. For infinity and not-a-number conversion style see notes.|^^|^^|^^|^^|^^|^^|^^|^^|^^|
|n|Returns the **number of characters written** so far by this call to the function.<br><br>The result is _written_ to the value pointed to by the argument. The specification may not contain any _flag_, _field width_, or _precision_.|_signed char*_|_short*_|_int*_|_long*_|_long long*_|_intmax_t*_|_signed intmax_t*_|_ptrdiff_t*_|N/A|
|p|Writes an implementation defined character sequence defining a **pointer**.|N/A|N/A|_void*_|N/A|N/A|N/A|N/A|N/A|N/A|
[Conversion Format Specifier table for `printf`]

> [!example]+ Example
> ```c
> #include <stdio.h>
> #include <stdint.h>
> #include <inttypes.h>
>  
> int main(void) {
>     const char* s = "Hello";
>     printf("Strings:\n"); // same as puts("Strings");
>     printf(" padding:\n");
>     printf("\t[%10s]\n", s);
>     printf("\t[%-10s]\n", s);
>     printf("\t[%*s]\n", 10, s);
>     printf(" truncating:\n");
>     printf("\t%.4s\n", s);
>     printf("\t%.*s\n", 3, s);
>  
>     printf("Characters:\t%c %%\n", 'A');
>  
>     printf("Integers:\n");
>     printf("\tDecimal:\t%i %d %.6i %i %.0i %+i %i\n",
>                          1, 2,   3, 0,   0,  4,-4);
>     printf("\tHexadecimal:\t%x %x %X %#x\n", 5, 10, 10, 6);
>     printf("\tOctal:\t\t%o %#o %#o\n", 10, 10, 4);
>  
>     printf("Floating point:\n");
>     printf("\tRounding:\t%f %.0f %.32f\n", 1.5, 1.5, 1.3);
>     printf("\tPadding:\t%05.2f %.2f %5.2f\n", 1.5, 1.5, 1.5);
>     printf("\tScientific:\t%E %e\n", 1.5, 1.5);
>     printf("\tHexadecimal:\t%a %A\n", 1.5, 1.5);
>     printf("\tSpecial values:\t0/0=%g 1/0=%g\n", 0.0/0.0, 1.0/0.0);
>  
>     printf("Fixed-width types:\n");
>     printf("\tLargest 32-bit value is %" PRIu32 " or %#" PRIx32 "\n",
> 										UINT32_MAX,     UINT32_MAX );
> }
> ```

[^1]: https://en.cppreference.com/w/c/io/fscanf
[^2]: https://en.cppreference.com/w/c/io/fprintf