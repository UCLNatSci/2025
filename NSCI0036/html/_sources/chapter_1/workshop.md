---
html_theme.sidebar_secondary.remove: true
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.18.1
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Workshop 1: Fundamentals

## Introduction to Programming

A computer program is a sequence of simple instructions that a computer can understand. Consider a hypothetical programming language *Natscithon* consisting of the following four instructions.

|Instruction|Meaning|
|---|---|
|**set x = ?**|Set the variable **x** to the value **?**|
|**display x**|Display the value of variable **x**|
|**increase x by ?**|Increase the value of **x** by **?**|
|**repeat while x > ?**<br/>&nbsp;&nbsp;&nbsp;&nbsp;**[...]**|Repeat the following instructions while **x > ?** |

For example, the following *Natscithon* program:
> **set x = 3**<br/>
> **repeat while x < 6**<br/>
> **&nbsp;&nbsp;&nbsp;&nbsp;increase x by 1**<br/>
> **&nbsp;&nbsp;&nbsp;&nbsp;display x**<br/>

will produce the following output:

> 4 <br/>
> 5 <br/>
> 6 <br/>

Check that you can understand why the program produces this output, then try the questions below. You will need pen and paper only for the questions in this section.

:::{exercise}
The following *Natscithon* program performs a calculation that you (probably) first learnt at primary school. What will the output of the program be? what is the calculation?

> **set x = 13**<br/>
> **repeat while x > 4**<br/>
> **&nbsp;&nbsp;&nbsp;&nbsp;increase x by -4**<br/>
> **display x**
:::

:::{exercise}
$13$ divided by $4$ is $3$ remainder $1$. We say that $3$ is the 'integer part' of the division.

Write a *Natscithon* program which calculates and displays the integer part of $13$ divided by $4$.

> **set x = 13**<br/>
> *...add your code here...*

Your program should produce the output:

> 3

*Hint: adapt the code in the previous question by adding a new variable to keep track of the number of times the repeated section of code is executed*.
:::

## Introduction to Python

In this section you'll be working with Python code. Before you start, create a new Jupyter Notebook.

We'll start with a simple example of a Python program which simulates the growth in population of a colony of bacteria. Suppose we start with 100 cells and the population doubles every hour. How many hours will it take to reach a population of 10000 cells?

```{code-cell} ipython3
pop = 100

while pop < 10000:
    # double the population
    pop = pop * 2
    print(pop)
```

Let's examine each line in turn. First, we define a **variable** `pop` and set its value to 100:

```
pop = 100
```

Then we define a `while` loop. A `while` loop repeats a section of code while the specified condition is true:

```
while pop < 10000:
```

The code in the indented block below this line is then executed repeatedly. The line `# double the population` is a comment and is ignored by the Python interpreter. Next, multiply `pop` by 2:

```
    pop = pop * 2
```

Then `print` the value of `pop`:

```
   print(pop)
```

Execution terminates once the condition `pop < 1000` becomes false.

When we run the code, we can see that it prints 7 values, so it must take 7 hours for the population to exceed 10000. But let's adapt the code so that it prints this number. We'll need to introduce a second variable to keep track of the number of hours:

+++

:::{exercise} 
:label: exercise_1_6
Replace the two comments in the code below so that it correctly prints the number of hours.
```{code-block} python
pop = 100
# set i to zero
while pop < 10000:
    pop = pop * 2
    # increase i by one
    print(pop)
    
print("Number of hours:", i)
```
:::

+++

Finally, suppose the the population growth rate is $1.02$ rather than $2$.

:::{exercise}
:label: exercise_1_7
Change the code above so that the growth rate is $1.02$.
:::

+++

Because the growth rate is much slower, we're getting to an enormous list of numbers. So let's print it only once every 24 hours instead.

:::{exercise}
:label: exercise_1_8
Replace the line

```
print(pop)
```

with

```
if i % 24 == 0:
    print(pop)
```
so that the population size is only displayed every 24 hours.
:::

+++


## Radioactive Decay

The half-life of a radioactive sample is the time taken for the activity of the sample (measured in Becquerels, Bq) to reduce by one-half. For example, Iodine-131 is a radioisotope with a half-life $t_\mathrm{half} = 8.02$ days. If a sample of I-131 has an initial activity of  $5.00 \times 10^{12}~\mathrm{Bq}$ then after $8.02$ days its activity will be $2.50 \times 10^{12}~\mathrm{Bq}$, and after $16.04$ days its activity will be  $1.25 \times 10^{12}~\mathrm{Bq}$ and so on.

In order to model the decay of Iodine-131 we first need to convert the half-life to the daily decay rate, i.e. the proportion of a sample that decays in one day. We can do this using the following formula:

$$r = \left(\frac{1}{2}\right) ^ {1/t_\mathrm{half}}$$

:::{exercise}
:label: exercise_1_9
Use the formula above to calculate the daily decay rate of Iodine-131.

```
half_life = 8.02
r = # your calculation 
```

:::

+++

Now let's suppose we have a sample of I-131 with an initial activity of $1.67 \times 10^{12}~\mathrm{Bq}$.

:::{exercise}
:label: exercise_1_10
Write a program which calculates the number of days it takes for the sample to reach an activity of $10000$ Becquerels. What is the activity after $8$ days? What value would you expect?
:::

+++

:::{exercise}
:label: exercise_1_11
Change your code so that it prints the activity of the sample once every 7 days.
:::

+++

## Pseudocode

Even for simple programs, it can be difficult to determine the sequence of Python commands required to correctly produce the desired outcome. One to way to make this process easier is to first write your program in **pseudocode**: human-readable instructions which describe the desired algorithm. The previous example might be expressed in pseudocode as follows:

:::{card}
Pseudocode Example
^^^
```{div} pseudocode
set r to half to the power 1/8.02  
set activity to 1.67 x 10^12  
set day to 0  
repeat until activity is less than 10000:  
&nbsp;&nbsp;&nbsp;&nbsp; multiply activity by r  
&nbsp;&nbsp;&nbsp;&nbsp; increase day by 1  
&nbsp;&nbsp;&nbsp;&nbsp; if day is divisible by 7:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; display activity
```
:::

There are no strict rules for writing pseudocode - the purpose is to assist you in turning an idea into working code, so you are free to write it in a manner which makes most sense to you. However, the following general rules are recommended.

 1. One line of pseudocode should translate to one line (possibly two lines) of Python code.
 2. Indent lines which are part of a repeated or conditional block.
 3. Do not include Python statements.
 4. Keep it simple, concise and readable.

 Pseudocode is a tool which you can use to help you break down the process of writing a program. When presented with a problem you would typically:

 1. Examine the problem and determine an algorithm to solve it
 2. Write down (using pen and paper) your algorithm in pseudocode 
 3. Check that your algorithm works by 'running' the pseudocode in your head (or with pen and paper)
 4. Convert the pseudocode to Python code and check that it works.

## The Collatz Problem
 
Given a positive integer $n$, the *Collatz Operation* is defined as follows:
    
 - If the $n$ is even, divide it by two
 - If the $n$ is odd, triple it and add one
 
Repeatedly applying the Collatz Operation results in a sequence of integers which eventually reaches the number 1.

For example, the *Collatz Sequence* for $n = 5$ is:

$$5, 16, 8, 4, 2, 1.$$

:::{exercise}
:label: exercise_1_12

Using pen and paper, write pseudocode for a program which prints the Collatz Sequence for $n = 5$.

:::

:::{exercise}
:label: exercise_1_13

Use your answer to the previous question to write a program which generates the Collatz Sequence for any given positive integer $n$. For example, 

```
n = 5

# your code to generate the Collatz Sequence
```

should produce the following:

```
5
16.0
8.0
4.0
2.0
1.0
```

:::

+++

Given a positive integer $n$, define the *Collatz Number* to be the length of the Collatz Sequence for $n$. For example, the Collatz number of 5 is 6.

:::{exercise}
:label: exercise_1_14
Write a program which calculates and prints the Collatz number of a given number $n$. For example, 

```
n = 5

# your code to generate the Collatz Number
```

should produce the following:

```
The Collatz number of 5 is 6
```
:::

+++

## Nested Loops

There are many cases when you want to have iteration happen within an iteration. In this case, we will “nest” our loops –- put one loop inside of another loop.

See if you can understand what the following code is doing. 

```{code-cell} ipython3
i = 1
while i <= 6:
    j = 1
    while j <= i:
        print(j, end="")
        j = j + 1
    print()
    i = i + 1
```

:::{exercise}
:label: exercise_1_16
Write a program which uses nested loops to print the following patterns:

a)
```
123456
12345
1234
123
12
1
```

b)
```
01010
10101
01010
10101
01010
```

c)
```
AAAAAB
AAAABB
AAABBB
AABBBB
ABBBBB
BBBBBB
```
:::

:::{exercise} Challenge
:label: exercise_1_15

Write a program which finds the smallest number $n$ whose Collatz Number is greater than 200.

:::

## Practice Exercises

The following exercises provide further practice of this week's material.

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
