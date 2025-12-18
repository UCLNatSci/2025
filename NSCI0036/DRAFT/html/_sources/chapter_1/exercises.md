# Exercises

:::{exercise}
:label: calculations_extra_digits

We can calculate how many digits there are in a number by repeatedly dividing by 10 until the number is less than one. The number of divisions is the number of digits in the number. For example, the number $8468$ has four digits:

$$8468 \div 10 = 846.8\\
846.8 \div 10 = 84.68\\
84.68 \div 10 = 8.468\\
8.468 \div 10 = 0.8468$$

1. Write pseudo-code for this calculation for a general number $n$.
2. Write a Python program to implement it, displaying the result in the format `1234 has 4 digits.`
3. Test your program with a variety of numbers.
4. Extend your program so that it works for negative numbers.

:::

:::{exercise}
:label: calculations_extra_factorial

Recall the definition of factorial of a number $n$,

$$n! = n \times (n-1) \times \ldots \times 2 \times 1.$$

We can calculate the factorial of $n$ by repeated multiplation.

Write pseudocode for this computation then write Python code that calculates the factorial of any given number.
:::

<!--

:::{exercise}
:label: calculations_extra_quadratic

Write a program which use the quadratic formula to print the solution to the quadratic equation $ax^2 + bx + c = 0$, given variables `a`, `b`, and `c`. Your program should print:

```
The solutions are x = 4 and x = 1
```
or
```
The solution is x = 1
```
or
```
There are no real solutions
```
(Hint: first calculate the discriminant $b^2-4ac$).
:::

:::{exercise}
:label: calculations_extra_division

Given two integers $n$ and $m$ it is possible to perform division-with-remainder by repeatedly subtracting $m$ from $n$ until the result is less than $m$. For example, to calculate 13 divided by 3:

13 - 3 = 10  
10 - 3 = 7  
7 - 3 = 4  
4 - 3 = 1  

13 divided by 3 equals 4 remainder 1.

1. Write pseudocode for a program which performs this calulation.  
2. Turn your pseudocode into a Python program. The result of the calculation should be displayed in words as above.

(hint: you'll need to create an extra variable to store the original value of `n`).

:::

0-->

:::{exercise}
:label: calculations_extra_duration
A duration `t` in seconds can be converted to days, hours, minutes and seconds using integer division:

1. Divide `t` by 60; set `t` to the quotient and call the remainder `s`.
1. Divide `t` by 60; set `t` to the quotient and call the remainder `m`.
1. Divide `t` by 24; set `d` to the quotient and call the remainder `h`.

Calculate the number of days, hours, minutes and seconds in one million seconds. Display the result as follows:
```
1000000 seconds is xx days H:M:S
```

:::

:::{exercise}
:label: calculations_extra_primes
A student has written the pseudocode below to test if a number $n$ is a prime number.
1. There are **two** errors in the pseudocode. Find them and fix them.
2. Use the corrected pseudocode to write Python code which tests if a whole number `n` is prime.
2. Extend your Python code so that it calculates the number of prime numbers strictly less than a given number `n`. For example, if `n = 7` then your program should print `3`  since there are three prime numbers strictly less than 7 (2, 3, and 5).

NB Python has keywords `True` and `False` which represent Boolean (True/False) values:
```
x = True
print(x)
```
:::

:::{card}
Prime number test
^^^
```{div} pseudocode
set value of n  
set result to True  
set i to 1  
repeat while i is less than n:  
&nbsp;&nbsp;&nbsp;&nbsp;if n is divisible by i  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; set result to False  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; increase i by 1  
display result
```
:::

:::{exercise}
:label: calculations_extra_gcd
The **Euclidean algorithm** is a method that will find the highest common factor (HCF) of two numbers. The HCF is the largest number that will evenly divide (wihout remainder) both values. For example, The HCF of 5 and 15 is 5.

Write Python code which calculates the HCF of two numbers `a` and `b`.

- identify the smaller value and subtract it from the larger value. Replace the larger number with the result of the subtraction.
- repeat the two steps until the values are equal. This value is the HCF of `a` and `b`.
:::
