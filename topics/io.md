Now that we are running a program, we want to be able to give input to our program and receive an output from it, right? So for that we need the I/O and in C, the functions we are going to use for I/O are defined in the `stdio.h` header file, and below is how to use them:

## Input
To take input from console, _`scanf` and variants[^1]_
  All the functions below are used to extract data and feed them into the variables whose address we pass into them. And they return the number of arguments successfully assigned before the first matching or input failure occurs.
1. `scanf(const char*restrict __fmt, addresses_of_variables)`: this function reads data from the `stdin` file and matches it the format string with string literals fed to it and puts the corresponding values into the variables whose address we have entered later in the respective order.
2. `sscanf(const char*restrict __s, const char*restrict __fmt, addresses_of_variables)`: this function is used to read the data from a character array passed as the first argument and the rest is same as `scanf`.
3. `fscanf(FILE*restrict __file, const char*restrict __fmt, addresses_of_variables)`: this function is used to read the content from a file by passing a file pointer and the later argument and behavior is same as `scanf`.

In the reference link above you can find how the format string is built.


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

In the reference link above you can find how the format string is built.

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


<hr style="width:80%;margin:auto">

Now that we have seen how to print something, an interesting add-on to it will be how we can control the cursor and customize the text we print. And that's done using the `ANSI` escape sequence codes. These were developed in the early era of computing when only terminal based interface existed and the manufacturers wanted to add something that makes the terminal more interactive and engaging. And from that the `ANSI` escape sequences were born.

There is a long list of these sequences which I might not be able to fit here, so I advice you to read up on them _here[^3]_ if you consider this to be useful.

[^1]: https://en.cppreference.com/w/c/io/fscanf
[^2]: https://en.cppreference.com/w/c/io/fprintf
[^3]: https://en.wikipedia.org/wiki/ANSI_escape_code