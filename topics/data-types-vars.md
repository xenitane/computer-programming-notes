The first thing we need to know is how computers store information, and the answer for that is the fundamental piece of information that electronics can hold, and that is called a bit. A bit can either be `0` or `1`. And when a the value of a bit is `1`, it's also said the bit is set or active and similar adjectives.

Now that's just 1 bit, but now how do we store more information, just use a collection of these bits, not like a number is represented by putting together that many set or unset bits. But rather by using a limited number of bits to represent a range of numbers under a certain convention that is writing them in binary notation.

The most fundamental unit of information is numbers, and we have a lot of different set of numbers:
$$
\begin{align}
\text{The set of natural numbers: }\mathbb{N}&=\{1,2,3,4,5,\dots\}\\ \\
\text{The set of prime numbers: }\mathbb{P}&=\{2,3,5,7,11,13,\dots\}\\
\text{The set of whole number: }\mathbb{W}&=\{0,1,2,3,4,5,\dots\}\\
\text{The set of integers: }\mathbb{Z}&=\{\dots,-5,-4,-3,-2,-1,0,1,2,3,4,5,\dots\}\\
\text{The set of rational number: }\mathbb{Q}&=\{-\frac{1}{2},\frac{5}{2},0.3333\dots,\frac{22}{7},\dots\}\\
\text{The set of irrational numbers: }\mathbb{F}&=\{\pi,\sqrt{2},e,0.12122122212222\dots,\dots\}\\
\text{The set of real numbers: }\mathbb{R}&=\mathbb{Q}\cup\mathbb{F}\\
\text{The set of complex numbers: }\mathbb{C}&=\{a+ib\mid a,b\in\mathbb{R};i=\sqrt{-1}\}
\end{align}
$$
And the most basic of these are the integers, and we can represent a certain range of those numbers using a fixed quantity of bits.

After this we have the notorious real numbers and they can also be written in binary form and they can be never ending considering the conversion of base from 10 to 2. But as we decided to use a fixed number of bits for numbers, so we'll have limited places after the decimal for their representation. But wait, what about numbers that are very small or very big, we want to store those too, right. So the computer scientists came up with a surprisingly good enough solution for this problem, as one of them said, how about using the scientific notation in binary format, which is like $(sign)* (2^p)*(1.0101111\dots)$.

Here, p can vary and the number we have can be doubled, quadrupled, halved, quartered, etc and we can just alter the binary number after the decimal for fine-tuning. So now we are just going to store 3 things, the `sign` of the number as a bit, the exponent `p`, and the part of number after the decimal up-to a certain precision like `l-bits` let's call it `b`. And finally the number from the stored information becomes $(-1)^{sign\_bit}*(1+\frac{b}{2^l})*2^p$. And the data is stored as: $\mid sign\_bit\mid exponant\mid mantisa\mid$. And this format is called the floating point number format.

And let's not forget all the different characters of the writing system like the alphabets, the mathematical symbols and other stuff, we need that too. So let's reserve a way of storing them too in a format called character.

So now we have counting numbers, fractions, characters. A complete guide on their sizes and ranges can be found [here](https://en.cppreference.com/w/c/language/arithmetic_types).

And there is still something left, we have instanced where we want to just have a type that doesn't denote anything, and as it's like this we call it void.

Also as we are using computers where we are gonna store some information, so we are gonna encounter situations where we would like to know the location where something is stored as well, and the type of variable we use for this purpose is called a pointer.

What would you like, write code for doing same things again and again or reuse code written once (obviously this), this is achieved by making functions and they also have a type which we'll see later.

And the way we usually declare a variable of these types in `C` is as follows:
```c
data_type variable_name /* = optional_initial_value */;

// example
char c;
int x=1;

// we can also make lists of elements of a particular type called an array as follows
data_type list_name[/*optional_capcity*/] /* = { optional_list_of_elements_coma_seperated_qty_less_than_or_equal_to_capacity } */;
// and these lists are usually stored in memory as a continuous big block divided into pieces for each element
```

> [!info] As the numbers are stored in bits, and we as humans use the decimal system, and computer scientists, mathematicians also have some other formats to represent numbers. We usually work with binary, octal, decimal, and hexadecimal number systems.

 And how we identify them is by a certain prefix on the number. The prefixes are:
 
| Base | Prefix    | Allowed-digits                    |
| ---- | --------- | --------------------------------- |
| 2    | 0b        | {0,1}                             |
| 8    | 0         | {0,1,2,3,4,5,6,7}                 |
| 10   | no-prefix | {0,1,2,3,4,5,6,7,8,9}             |
| 16   | 0x        | {0,1,2,3,4,5,6,7,8,9,a,b,c,d,e,f} | 

> [!note] in case of hexadecimal number we can also use capital letters instead of small but it is considered good practice to stick with one throughout.

example:

| binary    | octal | decimal   | hexadecimal    |
| :-------: | :-:   | :-------: | : -----------: |
| 11001     | 31    | 25        | 19             | 
| 1000001   | 101   | 65        | 41             |

And that's not it, there are a lot more types we can create just by using collection of same type or different types we mentioned above and the types we created earlier. And these collections are called [[data-structures.md|data structures]]. And we'll study them later in detail.
